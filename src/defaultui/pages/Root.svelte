<!-- Swiper styles must be global otherwise they are removed by the sass loader -->
<style type="text/scss" global>
    @import '../../../node_modules/swiper/swiper.scss';
	@import '../../../node_modules/swiper/components/navigation/navigation.scss';
	@import '../../../node_modules/swiper/components/pagination/pagination.scss';
	@import '../../../node_modules/swiper/components/scrollbar/scrollbar.scss';
</style>

<script lang="ts">
    import { ViewType } from "../viewtype";
    import IdentitySetup from "./IdentitySetup.svelte";
    import EditProfile from "./EditProfile.svelte";
    import { navigatedView } from "../localidstores";
    import type { NavigatedView } from "../navigatedview";
    import { onDestroy } from "svelte";
    import ManageIdentity from "./ManageIdentity.svelte";
    import ExportIdentity from "./ExportIdentity.svelte";

    export let activeView: NavigatedView = { viewType: ViewType.None };

    let unsubscriber = navigatedView.subscribe((newView)=>{
        activeView = newView;
    })

    onDestroy(()=>{
        unsubscriber();
    });
</script>

{#if activeView.viewType == ViewType.IdentitySetup }
<IdentitySetup></IdentitySetup>
{:else if activeView.viewType == ViewType.EditProfile }
<EditProfile></EditProfile>
{:else if activeView.viewType == ViewType.ManageIdentity }
<ManageIdentity></ManageIdentity>
{:else if activeView.viewType == ViewType.ExportIdentity }
<ExportIdentity></ExportIdentity>
{:else}
Nothing here
{/if}