<script>
  import { writable } from "svelte/store"
  import { setContext, onMount } from "svelte"
  import Component from "./Component.svelte"
  import NotificationDisplay from "./NotificationDisplay.svelte"
  import SDK from "../sdk"
  import {
    createDataStore,
    initialise,
    screenStore,
    notificationStore,
  } from "../store"

  // Provide contexts
  setContext("sdk", SDK)
  setContext("component", writable({}))
  setContext("data", createDataStore())
  setContext("screenslot", false)

  let loaded = false

  // Load app config
  onMount(async () => {
    await initialise()
    loaded = true
  })
</script>

{#if loaded && $screenStore.activeLayout}
  <Component definition={$screenStore.activeLayout.props} />
{/if}
<NotificationDisplay />
