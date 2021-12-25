<script>
    import {user} from "./sessionStore"
    import {supabase} from "./supabaseClient"
    import Auth from "./Auth.svelte"
	import Dashboard from './dashboard.svelte'
    import Profile from "./Profile.svelte"

    user.set(supabase.auth.user())

    supabase.auth.onAuthStateChange((_, session) => {
        user.set(session.user)
    })
</script>
<h1>HI</h1>
<div class="container" style="padding: 50px 0 100px 0;">
    {#if $user}
        <Profile />
		
    {:else}
        <Auth />
    {/if}
</div>