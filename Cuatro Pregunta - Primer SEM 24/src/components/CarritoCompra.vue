<template>
  <div class="container">
    <div class=" ">
      <div class="rou d-flex d-flex justify-content-center">
        <div class="col-4">
          <img
            class="img-fluid"
            alt="logo-cafeteria"
            src="https://picsum.photos/200/100"
          />
        </div>
        <div class="col-8">
          <h1>CAFETERIA EL BUEN SABOR</h1>
        </div>
      </div>

      <nav class="navbar navbar-expand bg-primary" data-bs-toggle="dark">
        <div class="container-fluid">
          <a class="navbar-brand" href="#">Navbar</a>
          <button
            class="navbar-toggler"
            type="button"
            data-bs-toggle="collapse"
            data-bs-target="#navbarSupportedContent"
            aria-controls="navbarSupportedContent"
            aria-expanded="false"
            aria-label="Toggle navigation"
          >
            <span class="navbar-toggler-icon"></span>
          </button>
          <div class="collapse navbar-collapse" id="navbarSupportedContent">
            <ul class="navbar-nav me-auto mb-2 mb-lg-0">
              <li class="nav-item">
                <a class="nav-link active" aria-current="page" href="#"
                  >Inicio</a
                >
              </li>
              <li class="nav-item">
                <a class="nav-link" href="#">Enlace</a>
              </li>
              <li class="nav-item dropdown">
                <a
                  class="nav-link dropdown-toggle"
                  href="#"
                  id="navbarDropdown"
                  role="button"
                  data-bs-toggle="dropdown"
                  aria-expanded="false"
                >
                  Dropdown
                </a>
                <ul class="dropdown-menu" aria-labelledby="navbarDropdown">
                  <li><a class="dropdown-item" href="#">Acción</a></li>
                  <li><a class="dropdown-item" href="#">Otra acción</a></li>
                  <li><hr class="dropdown-divider" /></li>
                  <li><a class="dropdown-item" href="#">Algo más aquí</a></li>
                </ul>
              </li>
              <li class="nav-item">
                <a class="nav-link disabled">Deshabilitado</a>
              </li>
            </ul>
            <form class="d-flex" role="search">
              <input
                class="form-control me-2"
                type="search"
                placeholder="Buscar"
                aria-label="Buscar"
              />
              <button class="btn btn-outline-success" type="submit">
                Buscar
              </button>
            </form>
          </div>
        </div>
      </nav>
    </div>
    <div class="row">
      <div class="col-6">
        <h1>Lista de productos</h1>
        <table class="table">
          <tbody>
            <tr>
              <th scope="col">#</th>
              <th scope="col">Nombre</th>
              <th scope="col">Descripcion</th>
              <th scope="col">Precio</th>
              <th scope="col">Imagen</th>
              <th scope="col">Acciones</th>
            </tr>
          </tbody>
          <tbody v-for="item in producto" :key="item.id">
            <tr>
              <th scope="row">{{ item.id }}</th>
              <td>{{ item.nombre }}</td>
              <td>{{ item.descripcion }}</td>
              <td>{{ item.precio }} bs.</td>
              <td>
                <img
                  src="../../public/img/cafeteria-cafe.jpg" alt="" class="img-fluid w-100"
                />
        
              </td>
              <td>
                <button class="btn btn-success" @click="addCart(item.id)">Agregar</button>
                <button class="btn btn-danger" @click="Eliminar(item.id)">
                  Eliminar
                </button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>

      <div class="col-6">

        <div class="row">
        <div v-for="viuw in itemCart" :key="viuw.id" class="card" style="width: 18rem">
          <img src="../../public/img/cafeteria-cafe.jpg" class="card-img-top" alt="..." />
          <div class="card-body">
            <h5 class="card-title">{{viuw.nombre}}</h5>
            <p class="card-text">
             {{viuw.descripcion}}
            </p>
              <p class="card-text">
             {{viuw.precio}}
            </p>
            <a href="#" class="btn btn-primary">Ir a algún lugar</a>
          </div>
        </div>
        <div class="d-flex d-flex justify-content-center row"></div>
        <h2>Carrito de compras</h2>
        <table class="table">
         <thead>
           <tr>
              <th scope="col">#</th>
              <th scope="col">Nombre</th>
              <th scope="col">Descripcion</th>
              <th scope="col">Precio</th>
              <th scope="col">Imagen</th>
         </tr>
       </thead>

        <tbody v-for="(suMrray,inde) in cartpush" :key="inde">
          <tr v-for="(item,subinde) in suMrray" :key="subinde">
            <th scope="row">{{item.id}} </th>
              <td>{{ item.nombre }}</td>
              <td>{{ item.descripcion }}</td>
              <td>{{ item.precio }} bs.</td>
              <td> <img src="../../public/img/cafeteria-cafe.jpg" alt="" class="img-fluid w-100"/></td>
           </tr>
        </tbody>
    </table>


        </div>

      </div>
  
    </div>
  </div>
</template>

<script>

import Productos from '../data/Productos'


export default {
  name: "CarritoCompra",
  data() {
    return {
    /*
      Produ: [
        {
          id: 1,
          nombre: "cafeteria-cafe",
          descripcion: "",
          precio: 5,
          imagen: "cafeteria-cafe.jpg",
        },
        {
          id: 2,
          nombre: "cafeteria-coffee",
          descripcion: "lorem10",
          precio: 15,
          imagen: "cafeteria-coffee.jpg",
        },
        {
          id: 3,
          nombre: "cafeteria-house",
          descripcion: "lorem10",
          precio: 25,
          imagen: "cafeteria-house.png",
        },
        {
          id: 4,
          nombre: "cafeteria-shop",
          descripcion: "lorem10",
          precio: 9,
          imagen: "cafeteria-shop.png",
        },
      
      
      ]
      */
      producto :null,
      itemCart:[],
      cartpush:[]

    }
  },
  mounted() {
    this.onload()
  },
  methods: {
    onload() {
      this.producto=Productos
    },

    Eliminar(id) {
      const saved = this.producto.filter((item) => item.id !== id);
      this.producto = [...saved];
    },
    addCart(id) {
      const cart = this.producto.filter((item) => item.id === id);
      this.Eliminar(id);
      this.itemCart=cart;
      //parte otra 
      this.cartpush.push(cart);
    }
  },
};
</script>
