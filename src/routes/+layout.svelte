<script lang="ts">
  // NEVER MOVE THIS INTO APP.CSS IT WILL BREAK
  // - cbble_
  import "../styles/app.css";
  import "../styles/fonts.css";

  import Sidebar from "$lib/sidebar/Sidebar.svelte";
  import Navbar from "../lib/Topbar.svelte";

  import { latestMCData, windowInfo } from "$lib/stores.svelte";
  import type { Snippet } from "svelte";
  import { innerWidth } from "svelte/reactivity/window";
  import type { PageData } from "./$types";
  interface Props {
    children: Snippet;
    data: PageData;
  }

  let { children, data }: Props = $props();

  latestMCData.packFormat = data.packFormat || 0;
  latestMCData.gameVersion = data.gameVersion || "1.0";

  windowInfo.width = innerWidth.current || 1920;
  windowInfo.isNavOpen = (innerWidth.current || 1920) >= 768;

  $effect(() => {
    console.log("%c📦 Datapack Wiki", `color: oklch(69.27% 0.2042 40.82); font-size: 24pt; font-weight: 600;`);
    console.log("If you know what you're doing here, and you want to help develop the wiki, contact a DPH admin.");
    console.log("Or just chill here, I'm a website, I can't stop you.");
  });
</script>

<div class="font-lexend h-full min-h-dvh flex flex-col text-stone-200">
  <Navbar />
  <div class="flex w-full h-[93%]">
    <Sidebar />
    <div id="content" class="py-12 w-full min-h-dvh text-stone-200 bg-stone-900">
      {@render children()}
    </div>
  </div>
</div>
