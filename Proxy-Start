/* ===== TMDEB Proxy ===== */
(function () {
    'use strict';

    var tmdb_proxy = {
      name: 'TMDB Proxy',
      version: '1.0.5',
      description: 'Проксирование постеров и API сайта TMDB',
      path_image: 'imagetmdb.com/',
      path_api: 'tmapi.' + (Lampa.Manifest && Lampa.Manifest.cub_domain ? Lampa.Manifest.cub_domain : 'cub.red') + '/3/'
    };

    Lampa.TMDB.image = function (url) {
      var base = Lampa.Utils.protocol() + 'image.tmdb.org/' + url;
      return Lampa.Storage.field('proxy_tmdb') ? Lampa.Utils.protocol() + tmdb_proxy.path_image + url : base;
    };

    Lampa.TMDB.api = function (url) {
      var base = Lampa.Utils.protocol() + 'api.themoviedb.org/3/' + url;
      return Lampa.Storage.field('proxy_tmdb') ? Lampa.Utils.protocol() + tmdb_proxy.path_api + url : base;
    };

    Lampa.Settings.listener.follow('open', function (e) {
      if (e.name == 'tmdb') {
        e.body.find('[data-parent="proxy"]').remove();
      }
    });
    console.log('TMDB-Proxy', 'started, enabled:', Lampa.Storage.field('proxy_tmdb'));

})();



/* ===== Start ===== */
(function () {
    'use strict';
    Lampa.Platform.tv();
    Lampa.Storage.set('protocol', 'http');
/* 
  if (Lampa.Storage.get('source') == 'cub') {
    Lampa.Storage.set('source', 'tmdb')
  }
*/
 document.addEventListener("DOMSubtreeModified", function(event) {
	var divs = document.getElementsByClassName("search__sources");
	var startSource = Lampa.Storage.get('source');
		if (divs.length > 0) {
			if (Lampa.Storage.get('source') == 'cub') {
				var startSource = Lampa.Storage.get('source');
				Lampa.Storage.set('mySource', startSource) // метка
				Lampa.Storage.set('source', 'tmdb');
			}
		} else {
		setTimeout(function(){
			if (localStorage.getItem('mySource')) {Lampa.Storage.set('source', Lampa.Storage.get('mySource'))}
			localStorage.removeItem("mySource");
		}, 1500)
	}
   }, false); 
    
    var pluginArray = Lampa.Storage.get('plugins');
    var delplugin = pluginArray.filter(function(obj) {return obj.url !== 'http://cub.red/plugin/tmdb-proxy'});
    Lampa.Storage.set('plugins', delplugin);

    var pluginArray = Lampa.Storage.get('plugins');
    var deleteplugin = pluginArray.filter(function(obj) {return obj.url !== 'https://cub.red/plugin/tmdb-proxy'});
    Lampa.Storage.set('plugins', deleteplugin);


    Lampa.TMDB.image = function (url) {
      var base = Lampa.Utils.protocol() + 'image.tmdb.org/' + url;
      return Lampa.Storage.field('proxy_tmdb') ? 'http://cors.lampa32.ru/proxy/' + Lampa.Utils.addUrlComponent(base) : base;
    };

    Lampa.TMDB.api = function (url) {
      var base = Lampa.Utils.protocol() + 'api.themoviedb.org/3/' + url;
      return Lampa.Storage.field('proxy_tmdb') ? 'http://cors.lampa32.ru/proxy/' + Lampa.Utils.addUrlComponent(base) : base;
    };

    Lampa.Settings.listener.follow('open', function (e) {
      if (e.name == 'tmdb') {
        e.body.find('[data-parent="proxy"]').remove();
      }
    });

      var dcma_timer = setInterval(function(){
	  if(typeof window.lampa_settings != 'undefined' && (window.lampa_settings.fixdcma || window.lampa_settings.dcma)){
		clearInterval(dcma_timer)
		if (window.lampa_settings.dcma)
			window.lampa_settings.dcma = false;
	  }
      },100);
	
    /*var dcma_timer = setInterval(function(){
      if(window.lampa_settings.dcma){
            clearInterval(dcma_timer)
            window.lampa_settings.dcma = false
      }
    },1000)*/

})();
