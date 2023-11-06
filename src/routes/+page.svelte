<script lang='ts'>
    import {onMount} from "svelte"

    const key = "6LcwZPsoAAAAAJqAdLMqs547sZR9DfMkl_t3WbGd"
    let State = {
        idle: 'idle',
        requesting: 'requesting',
        success: 'success'
    }
     let token: string = ''
     let state = State.idle

     const onSubmit = () => {
        state = State.requesting
        doRecaptcha()
     }

     const doRecaptcha = () => {
        grecaptcha.ready(function() {
            grecaptcha.execute(key, {action: 'submit '}).then(function(res) {
                state = State.success
                token = res
            })
        })
     }
     const onloadCallbak = () => {
        console.log('here')
     }
</script>
<svelte:head>
  <script src="https://www.google.com/recaptcha/api.js?render={key}" async defer></script>
  <script src="https://www.google.com/recaptcha/api.js?onload=onloadCallback&render=explicit"></script>
</svelte:head>
<h1>Recaptcha Tests</h1>
<div>state: {state}</div>
<br />
<div>token: {token.length > 0 ? token.slice(0,5) : 'none'}</div>
<main>
    <form on:submit|preventDefault={onSubmit}>
        <button type='submit'>submit</button>
    </form>
</main>
