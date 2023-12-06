<script>
	import Paint from "./Middleware/Paint.svelte"
	import Canvas from './Components/Canvas.svelte'
	import BottomPanel from "./Components/Footer.svelte"
	import TopPanel from "./Components/Header.svelte"

	window.addEventListener('beforeunload', function (event) {
    let confirmationMessage = 'Вы уверены, что хотите покинуть страницу?';

    (event || window.event).returnValue = confirmationMessage;
    alert(confirmationMessage);
    return confirmationMessage;
	});
</script>

<Paint>
	<TopPanel />
	<Canvas />
	<BottomPanel />
</Paint>

<style lang="scss">	
	:global(body) {
		user-select: none;
		margin: 0;
		padding: 0;
		min-height: 100vh;
		display: flex;
		justify-content: center;
		align-items: center;
		background: #e5e5e5;
	}
</style>