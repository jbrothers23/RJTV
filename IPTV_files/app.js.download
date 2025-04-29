document.addEventListener('contextmenu', event => event.preventDefault());
document.addEventListener('DOMContentLoaded', function() {
	const video = document.getElementById('drm-player');
	const searchBar = document.getElementById('search-bar');
	const channelsList = document.getElementById('channels');
	const uiContainer = document.getElementById('video-ott');
	document.addEventListener('DOMContentLoaded', (event) => {
		const openButton = document.getElementById('open-button');
		const sidebar = document.getElementById('sidebar');
		let inactivityTimer;
		let lastActivityTime = Date.now();
		const resetInactivityTimer = () => {
			lastActivityTime = Date.now();
			clearTimeout(inactivityTimer);
			inactivityTimer = setTimeout(() => {
				if (Date.now() - lastActivityTime >= 5000) {
					sidebar.classList.remove('open');
					openButton.style.display = 'block'
				}
			}, 5000)
		};
		const openSidebar = () => {
			sidebar.classList.add('open');
			openButton.style.display = 'none';
			resetInactivityTimer()
		};
		openButton.addEventListener('click', openSidebar);
		['mousemove', 'click', 'keypress'].forEach(eventType => {
			sidebar.addEventListener(eventType, resetInactivityTimer)
		})
	});
	const devtools = () => {
		const threshold = 160;
		const widthThreshold = window.outerWidth - window.innerWidth > threshold;
		const heightThreshold = window.outerHeight - window.innerHeight > threshold;
		if (widthThreshold || heightThreshold) {
			window.location.href = 'https://cignalplaytv.vercel.app/'
		}
	};
	devtools();
	window.addEventListener('resize', devtools);
	document.documentElement.addEventListener('click', function() {
		if (!document.fullscreenElement) {
			document.documentElement.requestFullscreen().catch(err => {})
		}
	});

	function checkOrientation() {
		if (window.innerHeight > window.innerWidth) {
			document.getElementById('container-ott').classList.remove('ott')
		} else {
			document.getElementById('container-ott').classList.add('ott')
		}
	}
	window.addEventListener('resize', checkOrientation);
	window.addEventListener('load', checkOrientation);
	const streams = {
		gma: {
			name: 'GMA',
			manifestUri: 'http://143.44.136.110:6910/001/2/ch00000090990000001093/manifest.mpd?virtualDomain=001.live_hls.zte.com',
		},
		anc: {
			name: 'ANC',
			manifestUri: 'https://cdn-ue1-prod.tsv2.amagi.tv/linear/amg01006-abs-cbn-anc-global-dash-abscbnono/index.mpd',
			licensekey: '4bbdc78024a54662854b412d01fafa16:6039ec9b213aca913821677a28bd78ae',
		},
		cinemaone: {
			name: 'CINEMA ONE',
			manifestUri: 'https://cdn-ue1-prod.tsv2.amagi.tv/linear/amg01006-abs-cbn-cinemaone-dash-abscbnono/index.mpd',
			licensekey: '58d0e56991194043b8fb82feb4db7276:d68f41b59649676788889e19fb10d22c',
		},
		cinemo: {
			name: 'CINEMO!',
			manifestUri: 'https://cdn-ue1-prod.tsv2.amagi.tv/linear/amg01006-abs-cbn-cinemo-dash-abscbnono/index.mpd',
			licensekey: 'aa8aebe35ccc4541b7ce6292efcb1bfb:aab1df109d22fc5d7e3ec121ddf24e5f',
		},
		gmapinoytv: {
			name: 'GMA PINOY TV',
			manifestUri: 'https://cdn-uw2-prod.tsv2.amagi.tv/linear/amg01006-abs-cbn-abscbn-gma-x7-dash-abscbnono/index.mpd',
			licensekey: 'c95ed4c44b0b4f7fa1c6ebbbbaab21a1:47635b8e885e19f2ccbdff078c207058',
		},
		kapamilyachannel: {
			name: 'KAPAMILYA CHANNEL',
			manifestUri: 'https://cdn-ue1-prod.tsv2.amagi.tv/linear/amg01006-abs-cbn-kapcha-dash-abscbnono/index.mpd',
			licensekey: 'bd17afb5dc9648a39be79ee3634dd4b8:3ecf305d54a7729299b93a3d69c02ea5',
		},
		myx: {
			name: 'MYX',
			manifestUri: 'https://cdn-ue1-prod.tsv2.amagi.tv/linear/amg01006-abs-cbn-myxnola-dash-abscbnono/index.mpd',
			licensekey: 'f40a52a3ac9b4702bdd5b735d910fd2f:5ce1bc7f06b494c276252b4d13c90e51',
		},
		teleradyoserbisyo: {
			name: 'TELERADYO SERBISYO',
			manifestUri: 'https://cdn-ue1-prod.tsv2.amagi.tv/linear/amg01006-abs-cbn-teleradyo-dash-abscbnono/index.mpd',
			licensekey: '47c093e0c9fd4f80839a0337da3dd876:50547394045b3d047dc7d92f57b5fb33',
		},
		tfc: {
			name: 'tfc',
			manifestUri: 'https://cdn-ue1-prod.tsv2.amagi.tv/linear/amg01006-abs-cbn-tfcasia-dash-abscbnono/index.mpd',
			licensekey: '9568cc84e1d944f38eac304517eab6fd:f12142af8f39b3bab79d3679d3665ebe',
		},
		tv5hd: {
			name: 'TV5 HD',
			manifestUri: 'https://qp-pldt-live-grp-02-prod.akamaized.net/out/u/tv5_hd.mpd',
			licensekey: '2615129ef2c846a9bbd43a641c7303ef:07c7f996b1734ea288641a68e1cfdc4d',
		},
		rptvhd: {
			name: 'RPTV HD',
			manifestUri: 'https://qp-pldt-live-grp-03-prod.akamaized.net/out/u/cnn_rptv_prod_hd.mpd',
			licensekey: '1917f4caf2364e6d9b1507326a85ead6:a1340a251a5aa63a9b0ea5d9d7f67595',
		},
		truefmtv: {
			name: 'True FM TV',
			manifestUri: 'https://qp-pldt-live-grp-08-prod.akamaized.net/out/u/truefm_tv.mpd',
			licensekey: '0559c95496d44fadb94105b9176c3579:40d8bb2a46ffd03540e0c6210ece57ce',
		},
		a2z: {
			name: 'A2Z',
			manifestUri: 'https://qp-pldt-live-grp-02-prod.akamaized.net/out/u/cg_a2z.mpd',
			licensekey: 'f703e4c8ec9041eeb5028ab4248fa094:c22f2162e176eee6273a5d0b68d19530',
		},
		ptv4: {
			name: 'PTV 4',
			manifestUri: 'https://qp-pldt-live-grp-02-prod.akamaized.net/out/u/cg_ptv4_sd.mpd',
			licensekey: '71a130a851b9484bb47141c8966fb4a3:ad1f003b4f0b31b75ea4593844435600',
		},
		ibc13: {
			name: 'IBC 13',
			manifestUri: 'https://qp-pldt-live-grp-07-prod.akamaized.net/out/u/ibc13_sd_new.mpd',
			licensekey: '16ecd238c0394592b8d3559c06b1faf5:05b47ae3be1368912ebe28f87480fc84',
		},
		buko: {
			name: 'Buko',
			manifestUri: 'https://qp-pldt-live-grp-06-prod.akamaized.net/out/u/cg_buko_sd.mpd',
			licensekey: 'd273c085f2ab4a248e7bfc375229007d:7932354c3a84f7fc1b80efa6bcea0615',
		},
		sarisari: {
			name: 'Sari-Sari',
			manifestUri: 'https://qp-pldt-live-grp-06-prod.akamaized.net/out/u/cg_sari_sari_sd.mpd',
			licensekey: '0a7ab3612f434335aa6e895016d8cd2d:b21654621230ae21714a5cab52daeb9d',
		},
		tvnmoviespinoy: {
			name: 'tvN Movies Pinoy',
			manifestUri: 'https://qp-pldt-live-grp-07-prod.akamaized.net/out/u/cg_tvnmovie.mpd',
			licensekey: '2e53f8d8a5e94bca8f9a1e16ce67df33:3471b2464b5c7b033a03bb8307d9fa35',
		},
		nbatvphilippines: {
			name: 'NBA TV Philippines',
			manifestUri: 'https://qp-pldt-live-grp-02-prod.akamaized.net/out/u/cgnl_nba.mpd',
			licensekey: 'c5e51f41ceac48709d0bdcd9c13a4d88:20b91609967e472c27040716ef6a8b9a',
		},
		premiersportshd: {
			name: 'Premier Sports HD',
			manifestUri: 'https://qp-pldt-live-grp-03-prod.akamaized.net/out/u/cg_ps_hd1.mpd',
			licensekey: 'b8b595299fdf41c1a3481fddeb0b55e4:cd2b4ad0eb286239a4a022e6ca5fd007',
		},
		onesportshd: {
			name: 'One Sports HD',
			manifestUri: 'https://qp-pldt-live-grp-07-prod.akamaized.net/out/u/cg_onesports_hd.mpd',
			licensekey: '53c3bf2eba574f639aa21f2d4409ff11:3de28411cf08a64ea935b9578f6d0edd',
		},
		pbarush: {
			name: 'PBA Rush',
			manifestUri: 'https://qp-pldt-live-grp-01-prod.akamaized.net/out/u/cg_pbarush_hd1.mpd',
			licensekey: '76dc29dd87a244aeab9e8b7c5da1e5f3:95b2f2ffd4e14073620506213b62ac82',
		},
		uaapvarsitychannel: {
			name: 'UAAP Varsity Channel',
			manifestUri: 'https://qp-pldt-live-grp-04-prod.akamaized.net/out/u/cg_uaap_cplay_sd.mpd',
			licensekey: '95588338ee37423e99358a6d431324b9:6e0f50a12f36599a55073868f814e81e',
		},
		onesportsplus: {
			name: 'One Sports+',
			manifestUri: 'https://qp-pldt-live-grp-03-prod.akamaized.net/out/u/cg_onesportsplus_hd1.mpd',
			licensekey: '322d06e9326f4753a7ec0908030c13d8:1e3e0ca32d421fbfec86feced0efefda',
		},
		tapsports: {
			name: 'Tap Sports',
			manifestUri: 'https://qp-pldt-live-grp-11-prod.akamaized.net/out/u/dr_tapsports.mpd',
			licensekey: 'eabd2d95c89e42f2b0b0b40ce4179ea0:0e7e35a07e2c12822316c0dc4873903f',
		},
		mptv: {
			name: 'MPTV',
			manifestUri: 'https://qp-pldt-live-grp-09-prod.akamaized.net/out/u/cg_mptv.mpd',
			licensekey: '6aab8f40536f4ea98e7c97b8f3aa7d4e:139aa5a55ade471faaddacc4f4de8807',
		},
		rockentertainement: {
			name: 'Rock Entertainment',
			manifestUri: 'https://qp-pldt-live-grp-13-prod.akamaized.net/out/u/dr_rockentertainment.mpd',
			licensekey: 'e4ee0cf8ca9746f99af402ca6eed8dc7:be2a096403346bc1d0bb0f812822bb62',
		},
		hitsnow: {
			name: 'HITS Now',
			manifestUri: 'https://qp-pldt-live-grp-09-prod.akamaized.net/out/u/cg_hitsnow.mpd',
			licensekey: '14439a1b7afc4527bb0ebc51cf11cbc1:92b0287c7042f271b266cc11ab7541f1',
		},
		taptv: {
			name: 'Tap TV',
			manifestUri: 'https://qp-pldt-live-grp-06-prod.akamaized.net/out/u/cg_taptv_sd.mpd',
			licensekey: 'f6804251e90b4966889b7df94fdc621e:55c3c014f2bd12d6bd62349658f24566',
		},
		globaltrekker: {
			name: 'Global Trekker',
			manifestUri: 'https://qp-pldt-live-grp-04-prod.akamaized.net/out/u/globaltrekker.mpd',
			licensekey: '5c26c24bce2942078cf6e35216632c2d:445887a1c0832ff457263d8bcadc993f',
		},
		warnertvhd: {
			name: 'Warner TV HD',
			manifestUri: 'https://qp-pldt-live-grp-05-prod.akamaized.net/out/u/cg_warnerhd.mpd',
			licensekey: '4503cf86bca3494ab95a77ed913619a0:afc9c8f627fb3fb255dee8e3b0fe1d71',
		},
		hgtvhd: {
			name: 'HGTV HD',
			manifestUri: 'https://qp-pldt-live-grp-08-prod.akamaized.net/out/u/hgtv_hd1.mpd',
			licensekey: 'f0e3ab943318471abc8b47027f384f5a:13802a79b19cc3485d2257165a7ef62a',
		},
		foodnetworkhd: {
			name: 'Food Network HD',
			manifestUri: 'https://qp-pldt-live-grp-09-prod.akamaized.net/out/u/cg_foodnetwork_hd1.mpd',
			licensekey: 'b7299ea0af8945479cd2f287ee7d530e:b8ae7679cf18e7261303313b18ba7a14',
		},
		fashiontvhd: {
			name: 'Fashion TV HD',
			manifestUri: 'https://qp-pldt-live-grp-11-prod.akamaized.net/out/u/dr_fashiontvhd.mpd',
			licensekey: '971ebbe2d887476398e97c37e0c5c591:472aa631b1e671070a4bf198f43da0c7',
		},
		axn: {
			name: 'AXN',
			manifestUri: 'https://qp-pldt-live-grp-06-prod.akamaized.net/out/u/cg_axn_sd.mpd',
			licensekey: 'fd5d928f5d974ca4983f6e9295dfe410:3aaa001ddc142fedbb9d5557be43792f',
		},
		lifetimesd: {
			name: 'Lifetime SD',
			manifestUri: 'https://qp-pldt-live-grp-11-prod.akamaized.net/out/u/dr_lifetime.mpd',
			licensekey: 'cf861d26e7834166807c324d57df5119:64a81e30f6e5b7547e3516bbf8c647d0',
		},
		hitshd: {
			name: 'Hits HD',
			manifestUri: 'https://qp-pldt-live-grp-04-prod.akamaized.net/out/u/hits_hd1.mpd',
			licensekey: 'dac605bc197e442c93f4f08595a95100:975e27ffc1b7949721ee3ccb4b7fd3e5',
		},
		hbohd: {
			name: 'HBO HD',
			manifestUri: 'https://qp-pldt-live-grp-03-prod.akamaized.net/out/u/cg_hbohd.mpd',
			licensekey: 'd47ebabf7a21430b83a8c4b82d9ef6b1:54c213b2b5f885f1e0290ee4131d425b',
		},
		hitsmovies: {
			name: 'HITS Movies',
			manifestUri: 'https://qp-pldt-live-grp-12-prod.akamaized.net/out/u/dr_hitsmovies.mpd',
			licensekey: 'f56b57b32d7e4b2cb21748c0b56761a7:3df06a89aa01b32655a77d93e09e266f',
		},
		tapmovieshd: {
			name: 'TAP Movies HD',
			manifestUri: 'https://qp-pldt-live-grp-06-prod.akamaized.net/out/u/cg_tapmovies_hd1.mpd',
			licensekey: '71cbdf02b595468bb77398222e1ade09:c3f2aa420b8908ab8761571c01899460',
		},
		rockaction: {
			name: 'Rock Action',
			manifestUri: 'https://qp-pldt-live-grp-13-prod.akamaized.net/out/u/dr_rockextreme.mpd',
			licensekey: '0f852fb8412b11edb8780242ac120002:4cbc004d8c444f9f996db42059ce8178',
		},
		tapactionflixhd: {
			name: 'Tap Action Flix HD',
			manifestUri: 'https://qp-pldt-live-grp-06-prod.akamaized.net/out/u/cg_tapactionflix_hd1.mpd',
			licensekey: 'bee1066160c0424696d9bf99ca0645e3:f5b72bf3b89b9848de5616f37de040b7',
		},
		hbofamilyhd: {
			name: 'HBO Family HD',
			manifestUri: 'https://qp-pldt-live-grp-03-prod.akamaized.net/out/u/cg_hbofam.mpd',
			licensekey: '872910c843294319800d85f9a0940607:f79fd895b79c590708cf5e8b5c6263be',
		},
		cinemaxhd: {
			name: 'Cinemax HD',
			manifestUri: 'https://qp-pldt-live-grp-01-prod.akamaized.net/out/u/cg_cinemax.mpd',
			licensekey: 'b207c44332844523a3a3b0469e5652d7:fe71aea346db08f8c6fbf0592209f955',
		},
		hbosignaturehd: {
			name: 'HBO Signature HD',
			manifestUri: 'https://qp-pldt-live-grp-01-prod.akamaized.net/out/u/cg_hbosign.mpd',
			licensekey: 'a06ca6c275744151895762e0346380f5:559da1b63eec77b5a942018f14d3f56f',
		},
		hbohitshd: {
			name: 'HBO Hits HD',
			manifestUri: 'https://qp-pldt-live-grp-09-prod.akamaized.net/out/u/cg_hbohits.mpd',
			licensekey: 'b04ae8017b5b4601a5a0c9060f6d5b7d:a8795f3bdb8a4778b7e888ee484cc7a1',
		},
		cnnhd: {
			name: 'CNN HD',
			manifestUri: 'https://qp-pldt-live-grp-12-prod.akamaized.net/out/u/dr_cnnhd.mpd',
			licensekey: '900c43f0e02742dd854148b7a75abbec:da315cca7f2902b4de23199718ed7e90',
		},
		oneph: {
			name: 'One PH',
			manifestUri: 'https://qp-pldt-live-grp-04-prod.akamaized.net/out/u/oneph_sd.mpd',
			licensekey: '92834ab4a7e1499b90886c5d49220e46:a7108d9a6cfcc1b7939eb111daf09ab3',
		},
		onenews: {
			name: 'One News',
			manifestUri: 'https://qp-pldt-live-grp-04-prod.akamaized.net/out/u/onenews_hd1.mpd',
			licensekey: 'd39eb201ae494a0b98583df4d110e8dd:6797066880d344422abd3f5eda41f45f',
		},
		bilyonaryoch: {
			name: 'Bilyonaryo News Channel',
			manifestUri: 'https://qp-pldt-live-grp-05-prod.akamaized.net/out/u/bilyonaryoch.mpd',
			licensekey: '227ffaf09bec4a889e0e0988704d52a2:b2d0dce5c486891997c1c92ddaca2cd2',
		},
		bloomberg: {
			name: 'Bloomberg',
			manifestUri: 'https://qp-pldt-live-grp-09-prod.akamaized.net/out/u/bloomberg_sd.mpd',
			licensekey: 'ef7d9dcfb99b406cb79fb9f675cba426:b24094f6ca136af25600e44df5987af4',
		},
		cna: {
			name: 'CNA',
			manifestUri: 'https://qp-pldt-live-grp-13-prod.akamaized.net/out/u/dr_channelnewsasia.mpd',
			licensekey: 'b259df9987364dd3b778aa5d42cb9acd:753e3dba96ab467e468269e7e33fb813',
		},
		aljazeera: {
			name: 'Al Jazeera',
			manifestUri: 'https://qp-pldt-live-grp-12-prod.akamaized.net/out/u/dr_aljazeera.mpd',
			licensekey: '7f3d900a04d84492b31fe9f79ac614e3:d33ff14f50beac42969385583294b8f2',
		},
		moonbugkids: {
			name: 'Moonbug Kids',
			manifestUri: 'https://qp-pldt-live-grp-06-prod.akamaized.net/out/u/cg_moonbug_kids_sd.mpd',
			licensekey: '0bf00921bec94a65a124fba1ef52b1cd:0f1488487cbe05e2badc3db53ae0f29f',
		},
		dreamworkstagalized: {
			name: 'DreamWorks (Tagalized)',
			manifestUri: 'https://qp-pldt-live-grp-07-prod.akamaized.net/out/u/cg_dreamworktag.mpd',
			licensekey: '564b3b1c781043c19242c66e348699c5:d3ad27d7fe1f14fb1a2cd5688549fbab',
		},
		animax: {
			name: 'Animax',
			manifestUri: 'https://qp-pldt-live-grp-07-prod.akamaized.net/out/u/cg_animax_sd_new.mpd',
			licensekey: '92032b0e41a543fb9830751273b8debd:03f8b65e2af785b10d6634735dbe6c11',
		},
		dreamworkshd: {
			name: 'DreamWorks HD',
			manifestUri: 'https://qp-pldt-live-grp-02-prod.akamaized.net/out/u/cg_dreamworks_hd1.mpd',
			licensekey: '4ab9645a2a0a47edbd65e8479c2b9669:8cb209f1828431ce9b50b593d1f44079',
		},
		nickelodeonsd: {
			name: 'Nickelodeon SD',
			manifestUri: 'https://qp-pldt-live-grp-11-prod.akamaized.net/out/u/dr_nickelodeon.mpd',
			licensekey: '9ce58f37576b416381b6514a809bfd8b:f0fbb758cdeeaddfa3eae538856b4d72',
		},
		historyhd: {
			name: 'History HD',
			manifestUri: 'https://qp-pldt-live-grp-11-prod.akamaized.net/out/u/dr_historyhd.mpd',
			licensekey: 'a7724b7ca2604c33bb2e963a0319968a:6f97e3e2eb2bade626e0281ec01d3675',
		},
		knowledgechannel: {
			name: 'Knowledge Channel',
			manifestUri: 'https://qp-pldt-live-grp-13-prod.akamaized.net/out/u/dr_knowledgechannel.mpd',
			licensekey: '0f856fa0412b11edb8780242ac120002:783374273ef97ad3bc992c1d63e091e7',
		},
		depedtv: {
			name: 'DepEd TV',
			manifestUri: 'https://qp-pldt-live-grp-07-prod.akamaized.net/out/u/depedch_sd.mpd',
			licensekey: '0f853706412b11edb8780242ac120002:2157d6529d80a760f60a8b5350dbc4df',
		},
		cgtn: {
			name: 'CGTN',
			manifestUri: 'https://qp-pldt-live-grp-04-prod.akamaized.net/out/u/cgtneng.mpd',
			licensekey: '2782770c21354914922efa9dbc82b513:cc65d298482da51046b0c0656f3f5f15',
		},
		cgtechstormtn: {
			name: 'TechStorm',
			manifestUri: 'https://qp-pldt-live-grp-11-prod.akamaized.net/out/u/dr_tech_storm.mpd',
			licensekey: '5675d85ce6754ba6aa8f6acc4660f76f:140bfb365cf143c349f68699238a610c',
		},
		tvnpremiumhd: {
			name: 'tvN Premium HD',
			manifestUri: 'https://qp-pldt-live-grp-09-prod.akamaized.net/out/u/cg_tvnpre.mpd',
			licensekey: 'e1bde543e8a140b38d3f84ace746553e:b712c4ec307300043333a6899a402c10',
		},
		kbsworldsd: {
			name: 'KBS World SD',
			manifestUri: 'https://qp-pldt-live-grp-12-prod.akamaized.net/out/u/dr_kbsworld.mpd',
			licensekey: '22ff2347107e4871aa423bea9c2bd363:c6e7ba2f48b3a3b8269e8bc360e60404',
		},
		nhkworldjapan: {
			name: 'NHK World Japan',
			manifestUri: 'https://qp-pldt-live-grp-12-prod.akamaized.net/out/u/dr_nhk_japan.mpd',
			licensekey: '3d6e9d4de7d7449aadd846b7a684e564:0800fff80980f47f7ac6bc60b361b0cf',
		},
		arirang: {
			name: 'Arirang',
			manifestUri: 'https://qp-pldt-live-grp-01-prod.akamaized.net/out/u/arirang_sd.mpd',
			licensekey: '13815d0fa026441ea7662b0c9de00bcf:2d99a55743677c3879a068dd9c92f824',
		},
		cctv4: {
			name: 'CCTV 4',
			manifestUri: 'https://qp-pldt-live-grp-12-prod.akamaized.net/out/u/dr_cctv4.mpd',
			licensekey: 'b83566836c0d4216b7107bd7b8399366:32d50635bfd05fbf8189a0e3f6c8db09',
		},
		abcaustralia: {
			name: 'ABC Australia',
			manifestUri: 'https://qp-pldt-live-grp-10-prod.akamaized.net/out/u/dr_abc_aus.mpd',
			licensekey: '389497f9f8584a57b234e27e430e04b7:3b85594c7f88604adf004e45c03511c0',
		},
		france24: {
			name: 'France 24',
			manifestUri: 'https://qp-pldt-live-grp-11-prod.akamaized.net/out/u/dr_france24.mpd',
			licensekey: '257f9fdeb39d41bdb226c2ae1fbdaeb6:e80ead0f4f9d6038ab34f332713ceaa5',
		},
		tv5monde: {
			name: 'TV5 Monde',
			manifestUri: 'https://qp-pldt-live-grp-11-prod.akamaized.net/out/u/dr_tv5_monde.mpd',
			licensekey: 'fba5a720b4a541b286552899ba86e38b:f63fa50423148bfcbaa58c91dfcffd0e',
		},
		bbcnews: {
			name: 'BBC News',
			manifestUri: 'https://qp-pldt-live-grp-04-prod.akamaized.net/out/u/bbcworld_news_sd.mpd',
			licensekey: 'f59650be475e4c34a844d4e2062f71f3:119639e849ddee96c4cec2f2b6b09b40',
		},
		animalplanet: {
			name: 'Animal Planet',
			manifestUri: 'https://qp-pldt-live-grp-02-prod.akamaized.net/out/u/cg_animal_planet_sd.mpd',
			licensekey: '436b69f987924fcbbc06d40a69c2799a:c63d5b0d7e52335b61aeba4f6537d54d',
		},
		bbcearthhd: {
			name: 'BBC Earth HD',
			manifestUri: 'https://qp-pldt-live-grp-03-prod.akamaized.net/out/u/cg_bbcearth_hd1.mpd',
			licensekey: '34ce95b60c424e169619816c5181aded:0e2a2117d705613542618f58bf26fc8e',
		},
		discovery: {
			name: 'Discovery Channel SD',
			manifestUri: 'https://qp-pldt-live-grp-13-prod.akamaized.net/out/u/dr_discovery.mpd',
			licensekey: 'd9ac48f5131641a789328257e778ad3a:b6e67c37239901980c6e37e0607ceee6',
		},
		asianfoodnetwork: {
			name: 'Asian Food Network',
			manifestUri: 'https://qp-pldt-live-grp-07-prod.akamaized.net/out/u/asianfoodnetwork_sd.mpd',
			licensekey: '1619db30b9ed42019abb760a0a3b5e7f:5921e47fb290ae263291b851c0b4b6e4',
		},
		travelchannel: {
			name: 'Travel Channel SD',
			manifestUri: 'https://qp-pldt-live-grp-08-prod.akamaized.net/out/u/travel_channel_sd.mpd',
			licensekey: 'f3047fc13d454dacb6db4207ee79d3d3:bdbd38748f51fc26932e96c9a2020839',
		},
		cartoonnethd: {
			name: 'Cartoon Network HD',
			manifestUri: 'https://qp-pldt-live-grp-12-prod.akamaized.net/out/u/dr_cartoonnetworkhd.mpd',
			licensekey: 'a2d1f552ff9541558b3296b5a932136b:cdd48fa884dc0c3a3f85aeebca13d444',
		},
		nickjr: {
			name: 'Nick JR',
			manifestUri: 'https://qp-pldt-live-grp-12-prod.akamaized.net/out/u/dr_nickjr.mpd',
			licensekey: 'bab5c11178b646749fbae87962bf5113:0ac679aad3b9d619ac39ad634ec76bc8',
		},
		crimeinvestigation: {
			name: 'Crime & Investigation',
			manifestUri: 'https://qp-pldt-live-grp-12-prod.akamaized.net/out/u/dr_crime_invest.mpd',
			licensekey: '21e2843b561c4248b8ea487986a16d33:db6bb638ccdfc1ad1a3e98d728486801',
		},
		kixhd: {
			name: 'Kix HD',
			manifestUri: 'https://qp-pldt-live-grp-06-prod.akamaized.net/out/u/kix_hd1.mpd',
			licensekey: 'a8d5712967cd495ca80fdc425bc61d6b:f248c29525ed4c40cc39baeee9634735',
		},
		thrill: {
			name: 'Thrill SD',
			manifestUri: 'https://qp-pldt-live-grp-06-prod.akamaized.net/out/u/cg_thrill_sd.mpd',
			licensekey: '928114ffb2394d14b5585258f70ed183:a82edc340bc73447bac16cdfed0a4c62',
		},
		pbo: {
			name: 'Pinoy Box Office (PBO)',
			manifestUri: 'https://qp-pldt-live-grp-04-prod.akamaized.net/out/u/pbo_sd.mpd',
			licensekey: 'dcbdaaa6662d4188bdf97f9f0ca5e830:31e752b441bd2972f2b98a4b1bc1c7a1',
		},
		vivacinema: {
			name: 'Viva Cinema',
			manifestUri: 'https://qp-pldt-live-grp-06-prod.akamaized.net/out/u/viva_sd.mpd',
			licensekey: '07aa813bf2c147748046edd930f7736e:3bd6688b8b44e96201e753224adfc8fb',
		},
		tmc: {
			name: 'Tagalog Movie Channel (TMC)',
			manifestUri: 'https://qp-pldt-live-grp-07-prod.akamaized.net/out/u/cg_tagalogmovie.mpd',
			licensekey: '96701d297d1241e492d41c397631d857:ca2931211c1a261f082a3a2c4fd9f91b',
		},
		premiersportshd: {
			name: 'Premier Sports HD',
			manifestUri: 'https://qp-pldt-live-grp-03-prod.akamaized.net/out/u/cg_ps_hd1.mpd',
			licensekey: 'b8b595299fdf41c1a3481fddeb0b55e4:cd2b4ad0eb286239a4a022e6ca5fd007',
		},
		spotvhd: {
			name: 'SPOTV HD',
			manifestUri: 'https://qp-pldt-live-grp-05-prod.akamaized.net/out/u/cg_spotvhd.mpd',
			licensekey: 'ec7ee27d83764e4b845c48cca31c8eef:9c0e4191203fccb0fde34ee29999129e',
		},
		spotv2hd: {
			name: 'SPOTV 2 HD',
			manifestUri: 'https://qp-pldt-live-grp-13-prod.akamaized.net/out/u/dr_spotv2hd.mpd',
			licensekey: '7eea72d6075245a99ee3255603d58853:6848ef60575579bf4d415db1032153ed',
		},
		tvmaria: {
			name: 'TV Maria',
			manifestUri: 'https://qp-pldt-live-grp-07-prod.akamaized.net/out/u/tvmaria_prd.mpd',
			licensekey: 'fa3998b9a4de40659725ebc5151250d6:998f1294b122bbf1a96c1ddc0cbb229f',
		},
		lotusmacau: {
			name: 'Lotus Macau',
			manifestUri: 'https://qp-pldt-live-grp-07-prod.akamaized.net/out/u/lotusmacau_prd.mpd',
			licensekey: '60dc692e64ea443a8fb5ac186c865a9b:01bdbe22d59b2a4504b53adc2f606cc1',
		},
		tvup: {
			name: 'TVUP',
			manifestUri: 'https://qp-pldt-live-grp-09-prod.akamaized.net/out/u/tvup_prd.mpd',
			licensekey: '83e813ccd4ca4837afd611037af02f63:a97c515dbcb5dcbc432bbd09d15afd41',
		},
		cnnhd: {
			name: 'CNN HD',
			manifestUri: 'https://qp-pldt-live-grp-03-prod.akamaized.net/out/u/cg_cnnhd.mpd',
			licensekey: '900c43f0e02742dd854148b7a75abbec:da315cca7f2902b4de23199718ed7e90',
		},
		premiersports2: {
			name: 'Premier Sports 2',
			manifestUri: 'https://qp-pldt-live-grp-13-prod.akamaized.net/out/u/dr_premiertennishd.mpd',
			licensekey: '59454adb530b4e0784eae62735f9d850:61100d0b8c4dd13e4eb8b4851ba192cc',
		}



//		kapamilyachannel: {
//			name: 'kapamilya channel',
//			manifestUri: 'https://cdn-ue1-prod.tsv2.amagi.tv/linear/amg01006-abs-cbn-kapcha-dash-abscbnono/index.mpd',
//			licenseserver: 'https://www.iwanttfc.com/api/1.0/license?itemID=ZfYR-ZQ9qH430EU3qU1XZQ&kid=BD17AFB5-DC96-48A3-9BE7-9EE3634DD4B8',
//		},
//		vice: {
//			name: 'vice',
//			manifestUri: 'https://dfwlive-v1-c1p2-sponsored.cf.dtvcdn.com/Content/HLS.cps/Live/channel(VICEHD-1936.dfw.1080)/index.m3u8',
//			licensekey: '6a7dd5c79fef1699ee2ffa3d38fe02b3:fac74244cd1383119f9f00a77ebbbde7',
//		},
//		cbsnewsdetroit: {
//			name: 'cbs news detroit',
//			manifestUri: 'https://cbsn-det.cbsnstream.cbsnews.com/out/v1/169f5c001bc74fa7a179b19c20fea069/master.m3u8',
//		},
	};
	const loadingOverlay = document.createElement('div');
	loadingOverlay.id = 'loading-overlay';
	loadingOverlay.style.position = 'absolute';
	loadingOverlay.style.top = '0';
	loadingOverlay.style.left = '0';
	loadingOverlay.style.width = '100%';
	loadingOverlay.style.height = '100%';
	loadingOverlay.style.backgroundColor = 'rgba(43, 51, 63, 0.7)';
	loadingOverlay.style.display = 'flex';
	loadingOverlay.style.justifyContent = 'center';
	loadingOverlay.style.alignItems = 'center';
	loadingOverlay.innerHTML = `<div class="circular-progress"><div class="circle"><div class="mask full"><div class="fill"></div></div><div class="mask half"><div class="fill"></div><div class="fill fix"></div></div></div><div class="inside-circle">0%</div></div>`;
	uiContainer.appendChild(loadingOverlay);
	const progressBarStyle = document.createElement('style');
	progressBarStyle.innerHTML = ``;
	document.head.appendChild(progressBarStyle);
	video.controls = false;
	const player = new gowatch.Player(video);
	video.addEventListener('pause', function() {
		video.play()
	});
	player.addEventListener('buffering', function(event) {
		if (event.buffering) {
			loadingOverlay.style.display = 'flex';
			startProgress()
		} else {
			loadingOverlay.style.display = 'none';
			stopProgress()
		}
	});
	player.addEventListener('error', onErrorEvent);
	let progressInterval;
	let progress = 0;

	function startProgress() {
		const progressBar = document.querySelector('.circular-progress .circle');
		const progressText = document.querySelector('.circular-progress .inside-circle');
		progressInterval = setInterval(() => {
			if (progress < 100) {
				progress += 1;
				const degree = (progress / 100) * 360;
				if (progress <= 50) {
					progressBar.querySelector('.mask.full').style.transform = `rotate(${degree}deg)`
				} else {
					progressBar.querySelector('.mask.full').style.transform = 'rotate(180deg)';
					progressBar.querySelector('.mask.half .fill').style.transform = `rotate(${degree-180}deg)`
				}
				progressText.innerText = `${progress}%`
			} else {
				clearInterval(progressInterval)
			}
		}, 50)
	}

	function stopProgress() {
		clearInterval(progressInterval);
		progress = 0;
		const progressBar = document.querySelector('.circular-progress .circle');
		const progressText = document.querySelector('.circular-progress .inside-circle');
		progressBar.querySelector('.mask.full').style.transform = 'rotate(0deg)';
		progressBar.querySelector('.mask.half .fill').style.transform = 'rotate(0deg)';
		progressText.innerText = '0%'
	}
	async function loadStream(stream) {
		let drmConfig = {
			servers: {},
			advanced: {
				'com.widevine.alpha': {
					videoRobustness: "SW_SECURE_CRYPTO",
					audioRobustness: "SW_SECURE_CRYPTO",
				}
			}
		};
		if (stream.licenseserver) {
			drmConfig.servers['com.widevine.alpha'] = stream.licenseserver
		}
		if (stream.licensekey) {
			const [licensekeyId, licensekeyValue] = stream.licensekey.split(':');
			drmConfig.drmkeys = {
				[licensekeyId]: licensekeyValue,
			}
		}
		player.configure({
			streaming: {
				abr: {
					enabled: false
				}
			},
			drm: drmConfig
		});
		if (stream.manifestUri.endsWith('.mpd')) {
			player.getNetworkingEngine().clearAllRequestFilters();
			player.getNetworkingEngine().registerRequestFilter((type, request) => {
				if (type === gowatch.net.NetworkingEngine.RequestType.SEGMENT) {
					const bandwidth = stream.bandwidth;
					request.allowCrossSiteCredentials = false;
					request.uris = request.uris.map(uri => uri + `?bandwidth=${bandwidth}`)
				}
			})
		} else {
			player.getNetworkingEngine().clearAllRequestFilters()
		}
		try {
			await player.load(stream.manifestUri)
		} catch (error) {
			onError(error)
		}
	}
	async function preloadStream(stream) {}

	function preloadAllStreams() {
		for (const licensekey in streams) {
			if (streams.hasOwnProperty(licensekey)) {
				preloadStream(streams[licensekey])
			}
		}
	}

	function populateChannelList() {
		channelsList.innerHTML = '';
		for (const licensekey in streams) {
			if (streams.hasOwnProperty(licensekey)) {
				const stream = streams[licensekey];
				const listItem = document.createElement('li');
				listItem.textContent = stream.name;
				listItem.addEventListener('click', () => loadStream(stream));
				channelsList.appendChild(listItem)
			}
		}
	}

	function onErrorEvent(event) {
		onError(event.detail)
	}

	function onError(error) {}
	searchBar.addEventListener('input', function(event) {
		const query = event.target.value.toLowerCase();
		channelsList.innerHTML = '';
		for (const licensekey in streams) {
			if (streams.hasOwnProperty(licensekey) && streams[licensekey].name.toLowerCase().includes(query)) {
				const stream = streams[licensekey];
				const listItem = document.createElement('li');
				listItem.textContent = stream.name;
				listItem.addEventListener('click', () => loadStream(stream));
				channelsList.appendChild(listItem)
			}
		}
	});
	preloadAllStreams();
	populateChannelList();
	loadStream(streams.tv5hd);
	const resolutionButton = document.createElement('button');
	resolutionButton.innerHTML = '<i class="fa fa-cog" style="color:white;"></i>';
	resolutionButton.style.position = 'absolute';
	resolutionButton.style.bottom = '40px';
	resolutionButton.style.right = '40px';
	resolutionButton.style.zIndex = '1001';
	resolutionButton.style.backgroundColor = 'rgba(255, 255, 255, 0)';
	resolutionButton.style.border = 'none';
	resolutionButton.style.fontSize = '24px';
	resolutionButton.style.cursor = 'pointer';
	uiContainer.appendChild(resolutionButton);
	const resolutionMenu = document.createElement('div');
	resolutionMenu.style.position = 'absolute';
	resolutionMenu.style.bottom = '40px';
	resolutionMenu.style.right = '20px';
	resolutionMenu.style.backgroundColor = 'rgba(43, 51, 63, 0.7)';
	resolutionMenu.style.color = '#fff';
	resolutionMenu.style.border = 'none';
	resolutionMenu.style.display = 'none';
	resolutionMenu.style.zIndex = '1001';
	uiContainer.appendChild(resolutionMenu);
	let timeoutId;

	function closeResolutionMenu() {
		resolutionMenu.style.display = 'none';
		resolutionButton.style.display = 'block';
		clearTimeout(timeoutId)
	}
	resolutionButton.addEventListener('click', () => {
		if (resolutionMenu.style.display === 'none') {
			resolutionMenu.style.display = 'block';
			resolutionButton.style.display = 'none';
			timeoutId = setTimeout(closeResolutionMenu, 5000)
		} else {
			closeResolutionMenu()
		}
	});

	function updateResolutions() {
		const tracks = player.getVariantTracks();
		const uniqueHeights = [...new Set(tracks.map(track => track.height))];
		const currentTrack = player.getVariantTracks().find(track => track.active);
		resolutionMenu.innerHTML = '';
		uniqueHeights.forEach(height => {
			const resOption = document.createElement('div');
			resOption.style.display = 'flex';
			resOption.style.alignItems = 'center';
			resOption.style.padding = '5px';
			resOption.style.cursor = 'pointer';
			const resText = document.createElement('span');
			resText.innerText = `${height}p`;
			const checkIcon = document.createElement('i');
			checkIcon.className = 'fa fa-check';
			checkIcon.style.marginLeft = '10px';
			checkIcon.style.visibility = currentTrack && currentTrack.height === height ? 'visible' : 'hidden';
			resOption.appendChild(resText);
			resOption.appendChild(checkIcon);
			resOption.addEventListener('click', () => {
				changeResolution(height);
				closeResolutionMenu()
			});
			resolutionMenu.appendChild(resOption)
		});
		const autoOption = document.createElement('div');
		autoOption.style.display = 'flex';
		autoOption.style.alignItems = 'center';
		autoOption.style.padding = '5px';
		autoOption.style.cursor = 'pointer';
		const autoText = document.createElement('span');
		autoText.innerText = 'Auto';
		const checkIconAuto = document.createElement('i');
		checkIconAuto.className = 'fa fa-check';
		checkIconAuto.style.marginLeft = '10px';
		checkIconAuto.style.visibility = currentTrack && !currentTrack.height ? 'visible' : 'hidden';
		autoOption.appendChild(autoText);
		autoOption.appendChild(checkIconAuto);
		autoOption.addEventListener('click', () => {
			changeResolution('Auto');
			closeResolutionMenu()
		});
		resolutionMenu.appendChild(autoOption)
	}

	function changeResolution(res) {
		const tracks = player.getVariantTracks();
		let selectedTrack = tracks[0];
		if (res !== 'Auto') {
			selectedTrack = tracks.find(track => track.height === res) || selectedTrack
		}
		player.selectVariantTrack(selectedTrack, true);
		player.configure({
			abr: {
				enabled: res === 'Auto'
			}
		});
		updateResolutions()
	}
	player.addEventListener('trackschanged', updateResolutions);
	updateResolutions()
});