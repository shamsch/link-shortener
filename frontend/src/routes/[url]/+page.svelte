<script>
// @ts-nocheck
    export let data;

    const isValidUrl = (url) => {
        const regex = /^(https?:\/\/)?([\da-z.-]+)\.([a-z.]{2,6})([/\w .-]*)*\/?$/;
        return regex.test(url);
    }
    const validUrl = isValidUrl(data.props.url);

    const makeAValidUrl = (url) => {
        if (url.startsWith('http://') || url.startsWith('https://')) {
            return url;
        }
        return `https://${url}`;
    }

    const redirectUser = (url) => {
        try {
            window.location.replace(makeAValidUrl(url));
        }
        catch (err) {
            console.log(err);
        }
    }

    setTimeout(() => {
        if (validUrl){ 
            redirectUser(data.props.url);
        }
    }, 3000);
    
</script>
  
<div class="container">
    {#if validUrl}
        <p> You are going to be redirected to <a href="{makeAValidUrl(data.props.url)}">{data.props.url}</a> </p>
        <p> If you are not redirected, click <a href="{makeAValidUrl(data.props.url)}">here</a> </p>
    {:else}
        <p> Invalid URL </p>
    {/if}
</div>

<style>
.container {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100vh;
    width: 100vw;
    background-color: #f5f5f5;
}

.container p{
    font-size: 1.5rem;
    font-weight: 500;
    margin-bottom: 1rem;
}

.container a{
    font-size: 1.5rem;
    font-weight: 500;
    margin-bottom: 1rem;
    color: #000;
}

</style>
