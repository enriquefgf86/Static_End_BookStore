<template><!--Vease que en vue todo se debe almacenar entre dos templates tags y actoseguido todo el contenido-->
    <div class='books'>      <!--qye aplicara al codigo debe estar enclasulado un un div tag(importante)-->
       <div class='flex-box-flip-container' >
        <div class='flip-card-container'>
            <div class='inner-flipper'>
             
                <div class='front-flip'>
                    <img style='width:200px;height:250px;border-radius:25px' v-bind:src='books.cover'>
                </div>
                <!--En Vue js CLI se empieza a usar un nuevo elemento cuyo prefijo(v)hace referencia a vue 
                el elemento (-bind) que se usaria para vincular un atributo html o elemto -->
                <div class='back-flip'>
                  <div class='data-items'>  
                    <h1 class='book-title'>{{books.title}}</h1><!--Vease que en este caso se utilizan parentesis
                    curlados para definir que dentro de ellos se va arrojar un resultado string o texto 
                    correspondiente al camino que de marca el denominador del objeto(books) en este caso (titles)-->
                    <a v-bind:href='books.cover '  v-bind:data-caption="books.description"  data-fancybox='gallery' >
                         <button class="button" > View More
                         </button>    
                         <img style='border-radius:25px' v-bind:src='books.detail' class="myBackImg"  >
                    </a>  
                 <!--Vease que en el caso anterior se usan v-bind  para anadir referencias(href)  y codigos(src)
                  al app, en el primer caso v-bind:href='books.cover' se hacde referencia a una imagen enclapsulada
                  en el objeto cover, (books se declara de antemano como camino indicador del objeto cual se quiere
                  indicar, y pudiese utilizarse cualquier otro nombre), vease qe este tag referencial enclapsula fancybooks 
                  plugins copiados previamnete de antemano desd esu cdn(data-caption) y (data-fancybox).
                  En el segundo caso al hacerse referencia a una imagen se utiliza el v-bind para apendizar un elemento
                  de un JSON file con propiedades png(imagen) de ahi que se utilice  --> 
                     
                  </div>   
                </div>
             </div >   
        </div>
       </div><!--Se cierra el flexbox-flip-container que alamcena los elementos y div con el efecto flip-->
    </div><!--Se cierra el div  que alamcena los elementos dentrodel template-->
</template><!--Se cierra el template que alamcena los elementos-->
<script>
export default {
    name:'books',
    props: {
      books:Object
    }
    
 }/*En esta parte del codigo se almacena todo codigo referente al javascript, y como concepto general del vuejsCLI,
 dentro de este script tag se debe hacer mencion a laos elementos a exportar al app principal mediante la clase 
 export default, vease que dentro de la misma se define primero el nombre de este componente(books), y alguna de sus
propiedades(props) , aunque en este caso simplemente se define  que dicha clase retornara o sera un objeto o conjunto de 
objetos , estas propiedades y nombres seran importadas desde el app principal para su compilacion y posterior muestreo 
 en el archivo index(html)*/
</script>
<style>
/*en este tag de styles iria todo lo rferente a css y embellecimiento del proyecto el cual pasaria a formar parte 
del app principal */

div.flip-card-container
{
    background-color: transparent;
    height: 250px;
    width:200px;
    perspective:1000px;
    padding-top:20px;
    
}
div.inner-flipper
{
    position: relative;
    height: 100%;
    width:100%;
    transition:transform 0.6s;
    text-align: center;
    transform-style:preserve-3d;
    box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
    
}
div.data-items
{
    display:flex;
    flex-direction:column;
    height:250px;
    width:200px;
    
}
div.flip-card-container:hover div.inner-flipper
{
transform:rotateY(180deg)
}
div.front-flip, div.back-flip
{
    position:absolute;
    height:100%;
    width:100%;
    backface-visibility: hidden;
    border-radius:15px;
    background-color: white;
}

div.back-flip
{

  color: white;
  transform: rotateY(-180deg);
  
}
h1.book-title
{
    color:white;
    background-color: rgba(2, 109, 16, 0.7);
    width:180px;
    border-radius: 10px 10px 10px 10px;
    font-size:17px;
    box-shadow: 1px 1px 1px 1px;
    margin:auto;
    border:solid;
    position:absolute;
    top:19px;
    margin-left:8px    
    
}
.myBackImg
{
    height:250px; 
    margin-top: 0;
    width:190px;
    position:relative;
    z-index: -3
    
}  
button.button
{
color:white;
width:100px;
font-weight: bold;
border-radius:10px 10px 10px 10px;
text-shadow:black;
background-color:rgb(1, 104, 23);
position:absolute;
top:195px;
margin-left:48px
} 

</style>