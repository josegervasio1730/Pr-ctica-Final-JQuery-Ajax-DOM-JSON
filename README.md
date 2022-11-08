Se modifico el archivo buscar.js, de tal manera que jalamos la api de las peliculas para poder hacer la consulta, 
esto fue posible con la estructura mostrada.


$.ajax({
	url: "http://api.themoviedb.org/3/search/movie?certification_country=MX&language=es&api_key=3356865d41894a2fa9bfa84b2b5f59bb&query="+palabra,
			success: function(respuesta) {

				setTimeout(function () {
					console.log(respuesta);
					miLista.empty();
					$.each(respuesta.results, function(index, elemento) {
						miLista.append(
							'<div class="media text-muted pt-3">'
	                        +  '<img style="max-width:50px;" class="mr-2 rounded" src="https://image.tmdb.org/t/p/w500' + elemento.poster_path + '"></img>'	
							+  '<p class="media-body pb-3 mb-0 small lh-125 border-bottom border-gray">'
							+    '<strong class="d-block text-gray-dark" data-toggle="modal" data-target="#modal'+index+'">'+elemento.title+'</strong>'
							+    elemento.overview
							+  '</p>'
	                        +'</div>'
							);  
						crearModal(index, elemento.overview);
			
					});
					miLista.slideDown("slow");
				}, 3000);

			},
			error: function() {
				console.log("No se ha podido obtener la información");
			},
			beforeSend: function() { 
				console.log('CARGANDO');
				miLista.empty();
				miLista.append('<div class="text-center"><img src="images/loading.gif" /></div>');
			},
		});

	});

});
 
Intente que se mostraran mas de 2 resultados, pero solo se logra mostrar 1 resultado similar a la busqueda. 

Autor: Cabañas Gervasio Jose Antonio. 
