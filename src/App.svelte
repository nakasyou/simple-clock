<script lang="ts">
  let h = 0
  let m = 0
  let s = 0

   const update = () => {
    const now = new Date()
    h = now.getHours() + (now.getMinutes() / 60)
    m = now.getMinutes()
    s = now.getSeconds()

    requestAnimationFrame(update)
  }
  update()

  const DEG_RAD = Math.PI / 180
  $: hRad = ((h % 12) / 12 * 360 - 90) * DEG_RAD
  $: mRad = (m / 60 * 360 - 90) * DEG_RAD
  $: sRad = (s / 60 * 360 - 90) * DEG_RAD
</script>
<main>
  <svg class="w-full" viewBox="0 0 512 512">
    <g>
      <circle cx="256" cy="256" r="5" />
    </g>
    <g>
      <line
        x1="256"
        y1="256"
        x2={Math.cos(hRad) * 130 + 256}
        y2={Math.sin(hRad) * 130 + 256} stroke="#000" />
    </g>
    <g>
      <line
        x1="256"
        y1="256"
        x2={Math.cos(mRad) * 200 + 256}
        y2={Math.sin(mRad) * 200 + 256} stroke="#000" />
    </g>
    <g>
      <circle cx={Math.cos(sRad) * 200 + 256} cy={Math.sin(sRad) * 200 + 256} r="10"></circle>
    </g>
    {#each [0,1,2,3,4,5,6,7,8,9,10,11,12].map(signal => [signal, signal * 30 * DEG_RAD]) as signal}
      <circle
        cx={Math.cos(signal[1]) * 200 + 256}
        cy={Math.sin(signal[1]) * 200 + 256} r="2"/>
    {/each}
  </svg>
</main>