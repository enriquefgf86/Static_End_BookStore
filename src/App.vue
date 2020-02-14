<template>
<div id="app">
 <div class ='body'> 
   <img class ='img' src='../public/zoom2.jpg' alt='zoom2'/>
  
    <Header @searchBar="getFilteredTitles" @droppers="getLanguage" v-bind:languagesSelected='getUniqueLanguage'></Header>
    <!--vease que este primer elemento enviado proveniente del header el cual consiste de dos parametros , el primero
    correspondiente al searchbar , y el segundo referente al filtro por lenguajes.
    en el caso del search bar vease que se recibe del componente header con @searchBar, y en este caspo se le pone el @
    como simbolo de recepcion del nombre , que en su momento fue emitido por el header($emit('searchBar....'), y se le
    asigna cualesquiera la funcion qiue asuma el elemento "getFilteredTitles", como el serach bar de antemano fue enviado
    con la variable search, que para su momento no tenia ninguna valor, aunque en el header se le apendizo un v-model
     dada sus caracteristicas de recibir y brindar informacion no se le especifica ningun bind o nada.
     el segundo elemento enviado desde el header fue 'droppers' mediante this.$emit("droppers",.....) el cual se le
     asigna cualesquiera el valor o funcion que represente el elemento 'getLanguage' en esta main App, correspondiente
     al dropdown selector con sus opciones,al pertenecer este elemnto al showmenu poseedor de varias opciones,entre
     ellas un loop sobre el array que este showmenu representaria , el cual seria las opciones a escoger, se le hace 
    un v-bind a dicho array proveniente como props del header('selectedLanguag') asignandole ademas 
    un atributo que devolveria  el elemento'getUniqueLanguage' -->
    <div class="card-flipping">
      <books v-for="(books,index) in filteredTitles" v-bind:key="index" v-bind:books="books" />
    </div>
    <!--Vesase que en esta parte se apendiza todo lo referente al componente books como proposito de mezclarlo con el
     componente headers y de esa manera venir conformando el app principal.
     En este caso al componente books , no presento ningun metodo o funcion a emitir al app principal, de ahi que 
      aunque en sus caracterisiticas solo se paso como un ojeto se inicia un loop sobre el retorno dado como array
      bookLists, en este caso transformado a filteredTitles despues de pasar por procesos de filtro.vease que isofacto
      se apendiza index al elemento key, y la propiedad como objeto de books proveniente del componente books -->

    <div class='conditional'>
        <div class='alert' v-if="filteredTitles.length==0"> {{Message.toUpperCase()}}</div>
    </div>
    <!--Vease que en este caso simplemente se estrablece un condicionante if sobre  el length del array
    filteredTitles , estableciendo que si es igual a 0, se debera mostrar un string  que encapsula el 
    elemento Message declarado como string en el retorno de la data dentro de los elementos export default.
    Vease que tambien se indica que dicho mensaje cualesquiera su formato debera se r expuesto todo en
    letras mayusculas de de ahi que se le indique mediante metodo toUppercase dicho proceder -->
  </div> 
  <div class='loader' v-if='loader'>
  </div>
 </div>  
</template>

<script>
import books from "./components/books.vue";
import Header from "./components/header.vue";
/*Vease que simplemente se importan ambos componentes books y Header, haciendose alusion especifica delos comonentes de
cual vienen "./components/books.vue" y ./components/header.vue respectivamente */
export default {
  name: "app",
  components: {
    Header,
    books
  },
  /*vease que se disponen los componentes recien importados como clara indicacion de su fusion con el main app Vue */
  data() {
    return {
      loader:false,
      bookLists: [],
      search: "",
      activeLanguage:'default',
      Message:'No Data.Try again your search please'
   /*En este  el elemento data tiene como retorno varias variables  o elementos , vease que el primero que se define
   es un array vacion llamdo bookLists, el cual mas abajo en el script sera el encargado de almacenar a traves de loop
   toda la data proveniente del Appi al cual se le hace un request mediante api, para posteriormente ser filtrado .
   el segundo elemento es search , que se define como un string vacio, pero que de antemano presenta uun background de 
   transferencia del componente header en donde se le apendiza un vmodel con las caracteristicas que esto implica...
   el tercer componente es una variable llamada activeLanguaje , la cual tiene un valor string por defecto, vease que
   esta variable corresponde a las opciones del showMenu  dropdwoselector tambien del header, donde aunque
   no aparace hay tambien un array que compondria otras opciones conformantes de este dropdown menu....
   El ultimo elemento  es una variable llamada  Message que almacena un string que previamente se explico se mostraria
   segun el condicionante if sobre el nuevo array filteredTitles  */   
    };
  },
  methods: {
    getJsonData() {
      fetch(" https://api.myjson.com/bins/zyv02 ", {
        method: "GET"
      })
        .then(response => {
          this.loader=true
          return response.json();
        })
        .then(bookStore => {
          this.loader=false
          this.bookLists = bookStore.books;
          console.log(bookLists)
        })
        .catch(error => {
          console.log(error);
        });
    },
    /*Vease que el primero de los metodos es getJsonData(), donde se resumen varios metodos para obtener el \
    json data asi como las posibles respuestas , y la orden concisa de almacenar dicho array de datos en la 
    variable previamente declarada como retorno de data bookLists */
    getFilteredTitles(text) {
      this.search = text;
    },
     /*este metodo seria el que se asigna al searchBar y los componentes importados por este concepto desde 
      el header, dada las caracteristicas de ese coponente impotrtado(el this.search correspondente al header component)
      no se desarrolla ninguna funcion aunque si se especifica que dicho metodo tendra como parametro un elemento,
      en este caso se le llamo texto(aunque pudiese haber sido cualesquiera otro nombre), y se le sera asignado como 
      valor al search del main app heredando todas las caracteristicas provenientes del componente header(incluyendo
      v-model funcion y demas)  */
    getLanguage: function(languages) {
      console.log(languages);
      this.activeLanguage = languages
    }
    /*El segundo metodo getLanguage en si encierra una funcion, cuyo parametro seria languages(aunque se le pudo haber 
    asignado cualquier otro), y al heredar todo lo proveniente del componente header , incluyendo su loop y su v-model
    vease que a diferencia del metdo anterior a este se le declara una funcion porque el elemento al cual se le asigna
     dicho metodo, droppers, proviene de un componente que ad iferencia del search(no legaba ningun valor) lega 
     un valor default ademas de sugerir loop sobre otro posible elemento que daria el array para elegir en la 
     segunda opcion */
  },
  computed: {
    filteredTitles: function() {
      return this.bookLists.filter(data => {
        return (data.title.toUpperCase().includes(this.search.toUpperCase())
        ||data.description.toUpperCase().includes(this.search.toUpperCase()));
      }).filter(data => (data.language == this.activeLanguage) || (this.activeLanguage === "default"))
    },
    /*A continuacion se declara la seccion de computed  en donde, la primera variable filteredTitles , pasaria a ser 
    el nuevo array a mostrar en el html una vez los criterios para los cuales se evalua el anterior array bookList
     se cumplen, vease que se le decalara una fucnion donde se filtra dicho array teniendo en centa el objeto titel,
     y para su ejecucion se necesitara incluir el elemento search con sus propiedades particulares y demas heredadas
      del componente header, y ademas como opcion or, se establece el mismo procedimiento pero esta vez evaluando el 
      array sobre el concepto description.Vease como otro retorno y nuevo filtro se apendiza en la misma funcion
      En este caso se evalua el retorno del json por concepto language , y se establece un if si el filtro por dicho
       concepto seria igual al activeLanguage en este momento(se debe tener en cuenta que el active language se compone
       de esta opcion default heradad mediante showMenu del componente header , ademas de el props a manera de array 
       languageSelected, el cual mediante la propiedad heredada @change retornaria valores que en combimacion con el 
        filtro anterior darian un resultado final), ademas de una opcion or, donde si la primera condicion no se cumple
         pues simepre retornar cualesquiera el valor bajo el concepto del activeLanguage igual a default  */
    
    getUniqueLanguage: function() {
      return Array.from(new Set(this.bookLists.map(data => data.language)));
    }
  },/*vease que en este segundo elemento del computed  se desarrolla una fucion que se le asigna a la variable
  getUniqueLanguage en donde como retorno se establece un metodo Array.from el cual simplemente crea un array sobre un 
  elemto sobre el cual se pueda iterar, de ahi que isofacto el elemento sobre el cual se aplica este Array.from llamado
  new Set, el cual devuelve una lista de elementos unicos no repetidos aunque diferente entre si, iterables, vease que
   esos elementos se sacarian del array bookLists mediante el metodo map sobre el elemento  language correspondiente a 
   dicho array    */
  created() {
    this.getJsonData();
  }
};
</script>

<style>
#app {
 margin-bottom:0;
  margin-top:0;
  margin-left:0px;
  margin-right:0;}
div.card-flipping {
  display: flex;
  flex-direction: row;
  width: 1100px;
  flex-wrap: wrap;
  margin: auto;
  justify-content: space-around;
  align-content: space-around;
  background-color: rgba(2, 109, 16, 0.7);
  padding: 17px;
  border-radius: 10px 10px 10px 10px;
}
.img{
  height:100%;
  width:100%;
  margin-left:0;
  z-index:-1;
  position:fixed;
}
div.alert
{
  color:white;
    background-color: rgba(2, 109, 16, 0.7);
    border-radius: 10px 10px 10px 10px;
    font-size:17px;
    box-shadow: 1px 1px 1px 1px;
    margin:auto;
    border:solid;
    position:center;
}
div.loader
{
  visibility:visible;
  width: 100px;
  height: 100px;

  border: 7px solid #f3f3f3;
  border-top:8px solid green;
  border-radius: 100%;

  

  animation-name: loader;
  animation-duration:  1s;
  animation-iteration-count:infinite;
  animation-timing-function: linear;
}
@keyframes loader {
  from {transform: rotate(0deg);} 
  to {transform: rotate(360deg);}
}

div.loader
{
  position: absolute;
  
  bottom:300px;
  left:0;
  right: 0;
  margin: auto;
}

</style>
