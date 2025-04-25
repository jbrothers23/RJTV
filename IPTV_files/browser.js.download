document.addEventListener('DOMContentLoaded', function() {
	const sidebar = document.getElementById('sidebar');
	const openButton = document.getElementById('open-button');
	const searchBar = document.getElementById('search-bar');
	const channelList = document.querySelector('.channel-sbr');
	let sidebarOpen = false;
	let touchTimeout;

	function openSidebar() {
		sidebar.classList.add('open');
		openButton.style.display = 'none';
		sidebarOpen = true;
		resetTouchTimeout()
	}

	function closeSidebar() {
		if (!searchBar.matches(':focus')) {
			sidebar.classList.remove('open');
			openButton.style.display = 'block';
			sidebarOpen = false;
			clearTimeout(touchTimeout)
		}
	}

	function resetTouchTimeout() {
		clearTimeout(touchTimeout);
		touchTimeout = setTimeout(closeSidebar, 3000)
	}

	function handleKeyDown(event) {
		if (sidebarOpen) {
			switch (event.key) {
				case 'ArrowUp':
					channelList.scrollTop -= 30;
					event.preventDefault();
					break;
				case 'ArrowDown':
					channelList.scrollTop += 30;
					event.preventDefault();
					break
			}
		}
	}
	openButton.addEventListener('click', openSidebar);
	sidebar.addEventListener('touchstart', function() {
		if (sidebarOpen) {
			resetTouchTimeout()
		}
	});
	sidebar.addEventListener('touchmove', function() {
		if (sidebarOpen) {
			resetTouchTimeout()
		}
	});
	sidebar.addEventListener('touchend', function() {
		if (sidebarOpen) {
			resetTouchTimeout()
		}
	});
	sidebar.addEventListener('mouseenter', function() {
		if (sidebarOpen) {
			resetTouchTimeout()
		}
	});
	sidebar.addEventListener('mouseleave', function() {
		if (sidebarOpen) {
			resetTouchTimeout()
		}
	});
	sidebar.addEventListener('mousemove', function() {
		if (sidebarOpen) {
			resetTouchTimeout()
		}
	});
	document.addEventListener('click', function(event) {
		if (sidebarOpen && !sidebar.contains(event.target) && !openButton.contains(event.target) && !searchBar.matches(':focus')) {
			closeSidebar()
		}
	});
	searchBar.addEventListener('focus', resetTouchTimeout);
	searchBar.addEventListener('input', resetTouchTimeout);
	channelList.addEventListener('scroll', function() {
		if (sidebarOpen) {
			resetTouchTimeout()
		}
	});
	document.addEventListener('keydown', handleKeyDown)
});