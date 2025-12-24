<script lang="ts">
import { onMount } from 'svelte'

interface Bubble {
 x: number
 y: number
 size: number
 speed: number
 opacity: number
 wobble: number
 mouseAttraction: number
 id: number
}

let container: HTMLDivElement
let canvas: HTMLCanvasElement
let ctx: CanvasRenderingContext2D
let bubbles: Bubble[] = []
let mouseX = 0
let mouseY = 0
let animationId: number
let bubbleIdCounter = 0
let catImage: HTMLImageElement

const BUBBLE_COUNT = 50
const BUBBLE_SPAWN_RATE = 0.3
const MOUSE_INFLUENCE_RADIUS = 150
const MOUSE_ATTRACTION_STRENGTH = 0.5

onMount(() => {
 if (!container) return
 
 canvas = container.querySelector('canvas') as HTMLCanvasElement
 ctx = canvas.getContext('2d')!
 
 // Set canvas size
 resizeCanvas()
 
 // Load cat image
 catImage = new Image()
 catImage.src = '/cat-svgrepo-com.svg'
 catImage.onload = () => {
  // Initialize bubbles after image loads
  for (let i = 0; i < BUBBLE_COUNT; i++) {
   createBubble()
  }
  
  // Start animation
  animate()
 }
 
 // Event listeners
 window.addEventListener('resize', resizeCanvas)
 container.addEventListener('mousemove', handleMouseMove)
 container.addEventListener('click', handleClick)
 
 return () => {
  cancelAnimationFrame(animationId)
  window.removeEventListener('resize', resizeCanvas)
  container.removeEventListener('mousemove', handleMouseMove)
  container.removeEventListener('click', handleClick)
 }
})

function resizeCanvas() {
 canvas.width = container.clientWidth
 canvas.height = container.clientHeight
}

function createBubble() {
 const bubble: Bubble = {
  x: Math.random() * canvas.width,
  y: canvas.height + 50,
  size: Math.random() * 30 + 10,
  speed: Math.random() * 2 + 1,
  opacity: Math.random() * 0.6 + 0.4,
  wobble: Math.random() * Math.PI * 2,
  mouseAttraction: 0,
  id: bubbleIdCounter++
 }
 bubbles.push(bubble)
}

function handleMouseMove(e: MouseEvent) {
 const rect = container.getBoundingClientRect()
 mouseX = e.clientX - rect.left
 mouseY = e.clientY - rect.top
}

function handleClick(e: MouseEvent) {
 const rect = container.getBoundingClientRect()
 const clickX = e.clientX - rect.left
 const clickY = e.clientY - rect.top
 
 // Check if any bubble was clicked
 for (let i = bubbles.length - 1; i >= 0; i--) {
  const bubble = bubbles[i]
  const distance = Math.sqrt((bubble.x - clickX) ** 2 + (bubble.y - clickY) ** 2)
  
  if (distance < bubble.size) {
   // Pop the bubble!
   bubbles.splice(i, 1)
   
   // Create pop effect
   createPopEffect(bubble.x, bubble.y)
   
   // Create a new bubble to replace it
   setTimeout(() => createBubble(), Math.random() * 1000)
   break
  }
 }
}

function createPopEffect(x: number, y: number) {
 // Create small sparkles
 for (let i = 0; i < 8; i++) {
  const sparkle = document.createElement('div')
  sparkle.style.position = 'absolute'
  sparkle.style.left = x + 'px'
  sparkle.style.top = y + 'px'
  sparkle.style.width = '4px'
  sparkle.style.height = '4px'
  sparkle.style.background = '#FFB6C1'
  sparkle.style.borderRadius = '50%'
  sparkle.style.pointerEvents = 'none'
  sparkle.style.zIndex = '1000'
  
  const angle = (i / 8) * Math.PI * 2
  const distance = 30 + Math.random() * 20
  const endX = x + Math.cos(angle) * distance
  const endY = y + Math.sin(angle) * distance
  
  sparkle.animate([
   { transform: 'translate(0, 0) scale(1)', opacity: '1' },
   { transform: `translate(${endX - x}px, ${endY - y}px) scale(0)`, opacity: '0' }
  ], {
   duration: 500,
   easing: 'ease-out'
  }).onfinish = () => sparkle.remove()
  
  container.appendChild(sparkle)
 }
}

function updateBubbles() {
 for (let i = bubbles.length - 1; i >= 0; i--) {
  const bubble = bubbles[i]
  
  // Move bubble up
  bubble.y -= bubble.speed
  
  // Add wobble motion
  bubble.wobble += 0.02
  bubble.x += Math.sin(bubble.wobble) * 0.5
  
  // Mouse attraction
  const dx = mouseX - bubble.x
  const dy = mouseY - bubble.y
  const distance = Math.sqrt(dx * dx + dy * dy)
  
  if (distance < MOUSE_INFLUENCE_RADIUS) {
   const force = (1 - distance / MOUSE_INFLUENCE_RADIUS) * MOUSE_ATTRACTION_STRENGTH
   bubble.x += (dx / distance) * force
   bubble.y += (dy / distance) * force * 0.3 // Less vertical attraction
  }
  
  // Remove bubbles that have floated off screen
  if (bubble.y < -50) {
   bubbles.splice(i, 1)
  }
 }
 
 // Spawn new bubbles occasionally
 if (Math.random() < BUBBLE_SPAWN_RATE && bubbles.length < BUBBLE_COUNT * 1.5) {
  createBubble()
 }
}

function drawBubbles() {
 ctx.clearRect(0, 0, canvas.width, canvas.height)
 
 for (const bubble of bubbles) {
  ctx.save()
  
  // Create gradient for bubble effect
  const gradient = ctx.createRadialGradient(
   bubble.x - bubble.size * 0.3,
   bubble.y - bubble.size * 0.3,
   0,
   bubble.x,
   bubble.y,
   bubble.size
  )
  
  gradient.addColorStop(0, `rgba(255, 255, 255, ${bubble.opacity * 0.8})`)
  gradient.addColorStop(0.7, `rgba(173, 216, 230, ${bubble.opacity * 0.4})`)
  gradient.addColorStop(1, `rgba(255, 182, 193, ${bubble.opacity * 0.2})`)
  
  ctx.fillStyle = gradient
  ctx.beginPath()
  ctx.arc(bubble.x, bubble.y, bubble.size, 0, Math.PI * 2)
  ctx.fill()
  
  // Draw cat image inside bubble if loaded
  if (catImage && catImage.complete) {
   const catSize = bubble.size * 1.2 // Cat slightly smaller than bubble
   ctx.globalAlpha = bubble.opacity * 0.8
   ctx.drawImage(
    catImage,
    bubble.x - catSize / 2,
    bubble.y - catSize / 2,
    catSize,
    catSize
   )
   ctx.globalAlpha = 1
  }
  
  // Add highlight
  ctx.fillStyle = `rgba(255, 255, 255, ${bubble.opacity * 0.6})`
  ctx.beginPath()
  ctx.arc(
   bubble.x - bubble.size * 0.3,
   bubble.y - bubble.size * 0.3,
   bubble.size * 0.3,
   0,
   Math.PI * 2
  )
  ctx.fill()
  
  ctx.restore()
 }
}

function animate() {
 updateBubbles()
 drawBubbles()
 animationId = requestAnimationFrame(animate)
}
</script>

<div bind:this={container} class="fixed inset-0 z-[-1]" aria-hidden="true">
 <canvas class="block w-full h-full"></canvas>
</div>

<style>
canvas{display:block;width:100%;height:100%;background:transparent!important}
</style>
