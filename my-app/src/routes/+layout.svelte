<script>
	import favicon from '$lib/assets/favicon.svg';
	
	let isOpen = $state(false);
	let activeItem = $state(1);
	
	const menuItems = [
		{ id: 1, label: 'Home', icon: '📊', href: '/' },
		{ id: 2, label: 'Create Ticket', icon: '👤', href: '/form' },
		{ id: 3, label: 'Settings', icon: '⚙️', href: '/settings' },
		{ id: 4, label: 'Messages', icon: '💬', href: '/messages' },
		{ id: 5, label: 'Logout', icon: '🚪', href: '/logout' }
	];
	
	function selectItem(id) {
		activeItem = id;
        isOpen = false;
	}

	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

<div class="sidebar" class:open={isOpen}>
	<button class="toggle" onclick={() => isOpen = !isOpen}>
		{isOpen ? '←' : '→'}
	</button>
	
<nav>
  {#each menuItems as item}
    <a class="menu-item" class:active={activeItem === item.id} href={item.href} onclick={() => selectItem(item.id)}>
      <span class="icon">{item.icon}</span>
      {#if isOpen}
        <span class="label">{item.label}</span>
      {/if}
    </a>
  {/each}
</nav>
</div>

{@render children?.()}

<style>
	:global(body) {
		margin-left: 75px;
	}
	
	.sidebar {
		position: fixed;
		left: 0;
		top: 0;
		height: 100vh;
		background: #2c3e50;
		transition: width 0.3s;
		width: 60px;
		display: flex;
		flex-direction: column;
		z-index: 100;
	}
	
	.sidebar.open {
		width: 200px;
	}
	
	.toggle {
		background: #34495e;
		color: white;
		border: none;
		padding: 1rem;
		cursor: pointer;
		font-size: 1.2rem;
	}
	
	nav {
		display: flex;
		flex-direction: column;
		flex: 1;
	}
	
	.menu-item {
		display: flex;
		align-items: center;
		gap: 1rem;
		padding: 1rem;
		background: transparent;
		border: none;
		color: white;
		cursor: pointer;
		text-align: left;
		text-decoration: none;
		transition: background 0.2s;
	}
	
	.menu-item:hover {
		background: #34495e;
	}
	
	.menu-item.active {
		background: #3498db;
	}
	
	.icon {
		font-size: 1.5rem;
		min-width: 28px;
	}
	
	.label {
		white-space: nowrap;
	}
</style>