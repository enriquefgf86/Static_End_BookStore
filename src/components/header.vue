<template>
  <div class='temp-header'>
    <div class="search-bar">
      <input type="text" @input="fitters()" v-model="search" placeholder="Search for Tittle or Description"/>
    </div>
    <!--vease que el primer elemento que se crea en este componente del app es un elemento input, que se presume 
    sea una barra de busqueda,se le especifica el tipo(como lo qie se le va a ingresar es tecto para inicializar
    el otor de busqueda se le determina text , y acto seguido se declara @input='fitters(), donde en la primera 
    parte de esta igualdad se refiere al envio(@)al main app del metodo, especificandose su tipo de interaccion
    en la aplicacion(input de texto), y en la segunda parte se hace referencia al metodo en si que se iria a 
    traspasar el cual se declaro como 'fitters()', vease que esto se origina en el script mas abajo....
    en el caso de 'v-model='search'', en la primera parte del elemento este v-model hace referencia a la
    propiedad 'two data binding' que no seria mas que la facultad que tiene n este elemento de hacer que su segundo
    componente sea actualizado cada vez que el usuario teclee o pulse  , almacnandose un nuevo valor, ese segundo 
    elemento seria ''search, el cual de antemano fue retornado i declarado con un valor nulo de ahi que es
    campo en blanco para que el cliente escriba lo que en si desee u ordene, y por consiguiente dicho valpor
     se almacenaria en el v-model como nuevo valor sobre el cual se aplicaraia cualesquiera la fucnion o metodo
      en si, ....
      y por ultimmos edeclara un elemento place holder es solo el texto que aparece en el input por defecto-->
    <div class="droppy">
      <select @change="droppies()" v-model="showMenu">
        <option value='default'>All</option>
        <option v-for="(lang, index) in languagesSelected" :value="lang" :key="index"  >
            <h1>{{lang.toUpperCase()}}</h1>
        </option>
      </select>
    </div>
      <!--Vease que en este segundo caso se pretende hacer un elemento dropdown el cual contendra varias opciones
      a seleccionar, vease que lo primero que se definen en el elemento es el tipo de funcion que lo triggeara, en ese
      caso se utilza @change, pues en su cambio entre opciones radica su ejecucion, y se le va a aasignar el
      metodo "droppies()"donde mas debajo en le script se explica su funcion, al igual que en el caso anterior 
      al ser un elemento del cual depende su intereccion con el usuario, se le creara un v-model donde en dependencia
      de la seleccion del usuario se ejecutara un cambio 'change' y por consiguiente se modificar un elemento cualesquiera
      que se declare en la  main app vinculado al anterior, vease que este a este elemento se le asigan a el valor asignado
      a la variable 'showMenu' en el retorno de la data, y como ya se explico anteriormente dicho valor cambiaria en 
      dependencia de su interccion con el usuario....
      ene este dropdown se declaran dos opciones sobre las cuales se seleccionara, la primera por defecto va a tener un 
      valor predewterminado llamado ''default'', el cual previamente ya se le fue asignado a la variable showMenu , y en la
      segunda opcion se estable un loop sobre un array llammado languagesSelected al cual se ace alusion en los componentes
      a exportar en el script , estableciendose como una propiedad que devolvera un array con valor String.Vease tambien
      que dicho objeto se le sera asignado a un valor (value)que en este caso por su naturleza una vez alojado en esa
      variable no cambiara como pasaria con un v-model, y como matriz de exposicion para dicho conjunto se va a apendizar
      el elemento html index mediante v-bind :key -->
    <div class="jumping">
            <h2>
                <span class="bouncers">
                  <span class="block1">
                    <span>b</span>
                    <span>o</span>
                    <span>o</span>
                    <span>k</span>
                  </span>    
                  <span class="block2">
                    <span>s</span>
                    <span>t</span>
                    <span>o</span>
                    <span>r</span>
                    <span>e</span>
                  </span> 
                </span>   
            </h2>
    </div>
  </div>
</template>
<script>
export default {
  name: "Header",
  data()
   {
    return{
      search: "",
      showMenu: "default"
    };
  },/*en la primera parte de los elementos que se exportan por defectpo vease que despues de declararse el nombre
    del componente name: "Header" se estable otro elemento qe seria data , el cual estableceria como retorno las 
    variables, search, de la cal se hablo anteriormente pertneeciente al tag input , y que por defecto iba, a tener 
    un placeholder con un texto predeterminado, y se le iba a apendizar un v-model debido a su natauraleza de recibir
    datos por el usuario para modificar un parametro y a la vez ser reiniciable para comenzar otro proceso con 
    nuevos valores y demas ; y el segundo variable seria showMenu='default' correspondiente al dropdownsellector
    en su condicion de establecer valor por defecto'default' , pues la segunda opcion seria un loop sobre array*/
  props: ["languagesSelected"],
    /*como se explico anteriormente la segunda opcion del dropdown selector vendria siendo el proceso de un loop sobre
    un array, especificamente un array de strings, y este elemento a exportar llamado props, declara en detalle
    las caracteristicas  y tipo del mismo un colectivo de elementos  String('') encerrados en un array []denominado
    languagesSelected */
  methods:
   {
    fitters()
     {
      this.$emit("searchBar", this.search);
    },
    /*y vease que en esta ultima parte se hace alusion a otra parte de los elementos que se exportarian, los metodos,
   uno llamdo fitters() al cual se hace alusion en el inicipo del header , dandosele como caracteristica que seria
   de tipo input , recibiendo el valor asigandao a la variable search(nulo en este caso)que dado su naturaleza se haria
   a travez de la apendizacion del v-model por sus carcateristicas de recibir y modificar datos de busquedas sin 
   un valor fijo  albergar, vease que 'searchBar', es el nombre que se le asigna para que pueda ser recibido por el 
   main app una vez sea expportado, y this.search , haria referencia al variable search retornado por data incluyendo
   sus caracteristicas de valor nulo .....siempre estos metodos para que puedan ser exportados se les debe poner 
   como prefijo this.$emit(this hace referencia a cualesquiera el valor variable o componente del componente en si 
   donde nos encontremos) */
    droppies()
    {   
      console.log(this.showMenu);
      this.$emit("droppers", this.showMenu);
    }
  }/*El segundo elemento de esta ultima parte vendria siendo lo mismo, aunque en esta caso haria referencia al
  la segunda parte del header en este caso el drop down selector que por sus caracteristicas de ser selectivo cuaando
   de sus opciones se elija una haria un cambio y por consiguiente una nueva evaluacion para es e cambio en si de ahi que se
   utilize @change , y dicho cambio se le asignaria lo correspondiente al metodo droppies, el cual al igual que 
    que en el caso anterior pasaria a ser exportado bajo el nombre de 'droppers', y su segundo elemento seria showmenu
    el cual por defecto posee un valor'default' aunque en dependencia de la interaccion del usuario podria variar y
    almacenar uno nuevo segun se cambie de ahi que en el header se apendize como v-model */
};
</script>
<style>
      div.temp-header
      {
        display:flex;
        flex-direction:row;
       width:800px;
        margin:auto;
        align-content: space-between;
        justify-content:flex-end;
      }
      select
      {
        right:110px;
        padding-left:15px;
      }
      input
      {
        width:300px;
        right:179px;
        font-weight: bold;
        text-align: center;
      }
      select,input
      {
        position:absolute;
        border-radius:10px;
        border:solid;
      }
      h2 {
    cursor: default;
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    width: 100%;
    height: 100px;
    margin: auto;
    display: block;
    text-align: center;
  }
  .jumping
  {
      position:absolute;
      top:100px;
      left:20px;
      
  }
  span.bouncers
  {
      display:flex;
      flex-direction: row;
      justify-content: space-between;
      width:110px;
  }
  
  h2 span 
  {
    position: relative;
    top: 20px;
    display: inline-block;
    animation: bounce 0.3s ease infinite alternate;
    font-size: 80px;
    color: #fff;
    text-shadow: 0 1px 0 #ccc, 0 2px 0 #ccc, 0 3px 0 #ccc, 0 4px 0 #ccc,
      0 5px 0 #ccc, 0 6px 0 transparent, 0 7px 0 transparent, 0 8px 0 transparent,
      0 9px 0 transparent, 0 10px 10px rgba(0, 0, 0, 0.4);
  }
  
  h2 span:nth-child(2) {
    animation-delay: 0.1s;
  }
  
  h2 span:nth-child(3) {
    animation-delay: 0.2s;
  }
  
  h2 span:nth-child(4) {
    animation-delay: 0.3s;
  }
  
  h2 span:nth-child(5) {
    animation-delay: 0.4s;
  }
  
  h2 span:nth-child(6) {
    animation-delay: 0.5s;
  }
  
  h2 span:nth-child(7) {
    animation-delay: 0.6s;
  }
  
  h2 span:nth-child(8) {
    animation-delay: 0.2s;
  }
  
  h2 span:nth-child(9) {
    animation-delay: 0.3s;
  }
  
  h2 span:nth-child(10) {
    animation-delay: 0.4s;
  }
  
  h2 span:nth-child(11) {
    animation-delay: 0.5s;
  }
  
  h2 span:nth-child(12) {
    animation-delay: 0.6s;
  }
  
  h2 span:nth-child(13) {
    animation-delay: 0.7s;
  }
  
  h2 span:nth-child(14) {
    animation-delay: 0.8s;
  }
  
  /* ANIMATION */
  @keyframes bounce 
  {
    100% 
    {
      top: -20px;
      text-shadow: 0 1px 0 #ccc, 0 2px 0 #ccc, 0 3px 0 #ccc, 0 4px 0 #ccc,
        0 5px 0 #ccc, 0 6px 0 #ccc, 0 7px 0 #ccc, 0 8px 0 #ccc, 0 9px 0 #ccc,
        0 50px 25px rgba(0, 0, 0, 0.2);
    }
  }

</style>