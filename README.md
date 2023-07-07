# Pokedex-Explaination

¡Entendido! A continuación, proporcionaré una explicación más detallada de cada bloque de código, presentando cada bloque visualmente y brindando una explicación conceptual junto con un glosario de términos al final.

    Bloque de código 3:

```typescript

export interface AppTypeInitialState { }

export interface PokemonTypeInitialState {
    allPokemon: undefined | genericPokemonType[];
}

export interface genericPokemonType {
    name: string;
    url: string;
}
```

En este bloque de código se definen tres interfaces: AppTypeInitialState, PokemonTypeInitialState y genericPokemonType. Estas interfaces permiten definir la estructura y el tipo de datos utilizados en otros bloques de código. 
°Este bloque de código define las interfaces AppTypeInitialState, PokemonTypeInitialState y genericPokemonType, que representan la estructura de datos utilizada en la aplicación.
En este bloque de código se definen tres interfaces: AppTypeInitialState, PokemonTypeInitialState y genericPokemonType.
La interfaz AppTypeInitialState no tiene propiedades definidas.
La interfaz PokemonTypeInitialState tiene una propiedad llamada allPokemon, que puede ser undefined o un arreglo de genericPokemonType.
La interfaz genericPokemonType define las propiedades name y url como cadenas de texto.

Glosario de términos:

    Interface: En TypeScript, una interfaz es una forma de definir la estructura de un objeto. Permite definir los nombres de las propiedades y los tipos de datos que deben tener.

~~A continuación, se presenta un glosario de términos utilizados en este bloque:

Interface: En TypeScript, una interfaz es una forma de definir la estructura de un objeto. Permite definir los nombres de las propiedades y los tipos de datos que deben tener. En este caso, se definen interfaces para representar el estado inicial de la aplicación (AppTypeInitialState y PokemonTypeInitialState) y el tipo de objeto utilizado para representar un Pokémon (genericPokemonType).

    Bloque de código 7:

```typescript

import React, { useEffect } from 'react';
import Wrapper from '../sections/Wrapper';
import { useAppDispatch, useAppSelector } from '../app/hooks';
import { getInitialPokeData } from '../app/reducers/getInitialPokeData';
import { getPokeData } from '../app/reducers/getPokeData';

function Search() {
    const dispatch = useAppDispatch();
    const {allPokemon} = useAppSelector(({pokemon})=>pokemon)
    useEffect (()=> {
        dispatch(getInitialPokeData());
    }, [dispatch]);
    useEffect (()=>{
        if(allPokemon) {
            const clonedPokemons = [...allPokemon];
            const randomPokemonsId = clonedPokemons
                .sort(()=> Math.random() - Math.random())
                .slice(0, 20);
            console.log(randomPokemonsId);
            dispatch(getPokeData(randomPokemonsId));
        }

    },[allPokemon, dispatch]);
    return (
        <div></div>
    );
}

export default Wrapper(Search);
```

°    Este bloque de código define la función Search, que es un componente de React. La acción que se realiza al ejecutarse es:

    useEffect (1ª ejecución):
        La función useEffect se ejecuta cuando el componente Search se monta.
        La acción realizada es dispatch(getInitialPokeData()).
        Esta acción invoca la función asíncrona getInitialPokeData, que realiza una solicitud HTTP GET utilizando axios.get a pokemonsRoute y captura los datos de la respuesta en data.
        Luego, se muestra data en la consola.
        Finalmente, se devuelve data.results.

    useEffect (2ª ejecución):
        La función useEffect se ejecuta cuando allPokemon cambia.
        Si allPokemon tiene un valor, se realizan las siguientes acciones:
            Se crea una copia de los pokémon en clonedPokemons utilizando el operador spread [...allPokemon].
            Los pokémon en clonedPokemons se ordenan de manera aleatoria utilizando el método sort() y una función de comparación ()=> Math.random() - Math.random().
            Se seleccionan los primeros 20 pokémon mediante el método slice(0, 20).
            Se muestra por consola randomPokemonsId.
            Se realiza la acción dispatch(getPokeData(randomPokemonsId)), que invoca la función asíncrona getPokeData.

    Bloque de código 2:

```typescript

import { configureStore, ThunkAction, Action } from '@reduxjs/toolkit';
import { AppSlice } from './slices/AppSlice';
import { PokemonSlice } from './slices/PokemonSlice';

export const store = configureStore({
  reducer: {
    app: AppSlice.reducer,
    pokemon: PokemonSlice.reducer,
  },
});

export type AppDispatch = typeof store.dispatch;
export type RootState = ReturnType<typeof store.getState>;
export type AppThunk<ReturnType = void> = ThunkAction<
  ReturnType,
  RootState,
  unknown,
  Action<string>
>;
```
En este bloque de código se configura la tienda de Redux utilizando la función configureStore de Redux Toolkit. También se definen los tipos AppDispatch, RootState y AppThunk que se utilizan en otros bloques de código. 

°Este bloque de código configura la tienda de Redux utilizando configureStore y define los tipos AppDispatch, RootState y AppThunk. No realiza ninguna acción directa, solo configura la tienda y define los tipos.
°Este bloque de código importa la función configureStore, los tipos ThunkAction y Action, y los slices AppSlice y PokemonSlice de sus respectivos archivos. Luego, se configura la tienda de Redux utilizando configureStore, se definen los tipos AppDispatch, RootState y AppThunk, y se exporta la tienda store.

Glosario de términos:

    configureStore: configureStore es una función de @reduxjs/toolkit que se utiliza para crear la tienda de Redux.
    ThunkAction: ThunkAction es un tipo de dato utilizado en Redux para representar acciones asíncronas.
    Action: Action es un tipo de dato utilizado en Redux para representar una acción.
    AppSlice: AppSlice es un slice de Redux que contiene los reducers y las acciones relacionadas con la aplicación.
    PokemonSlice: PokemonSlice es un slice de Redux que contiene los reducers y las acciones relacionadas con los pokemones.


~~A continuación, se presenta un glosario de términos utilizados en este bloque:

Store: En Redux, la tienda (store) es el objeto central que contiene el estado de la aplicación. La tienda es responsable de recibir las acciones, invocar los reducers correspondientes y actualizar el estado en consecuencia. En este bloque, la tienda se configura utilizando configureStore.

Reducer: Un reducer es una función que especifica cómo se actualiza el estado de la aplicación en respuesta a una acción. En este bloque, se importan los reducers AppSlice.reducer y PokemonSlice.reducer desde los archivos correspondientes y se los asigna a las propiedades app y pokemon del objeto reducer en la configuración de la tienda.

Dispatch: En Redux, dispatch es una función utilizada para enviar acciones a la tienda. Permite que las acciones se procesen y actualicen el estado de la aplicación. En este bloque, se define el tipo AppDispatch, que representa el tipo de la función dispatch de la tienda.

RootState: El RootState es el tipo de dato que representa el estado raíz de la aplicación. En este bloque, se define el tipo RootState como el tipo de retorno de la función store.getState(), que proporciona el estado actual de la tienda.

ThunkAction: ThunkAction es un tipo de dato utilizado en Redux para representar acciones asíncronas. Define los tipos de retorno, el tipo del estado raíz y el tipo de argumentos adicionales utilizados por las acciones asíncronas. En este bloque, se define el tipo AppThunk utilizando ThunkAction.

     Bloque de código 6:

```typescript

import { createAsyncThunk } from "@reduxjs/toolkit";
import { genericPokemonType } from "../../utils/Types";

export const getPokeData = createAsyncThunk("pokemon/randomPokemon",
    async (pokemons: genericPokemonType[]) => {
        try{
            console.log({pokemons},"from reducer");
        }catch(err){}
    }
```


°Este bloque de código define la acción asíncrona getPokeData utilizando createAsyncThunk. En este bloque en particular, no se ejecuta ninguna acción específica. Solo se muestra un mensaje en la consola, pero esto se considera un efecto secundario y no tiene un impacto directo en el flujo de ejecución.
°Este bloque de código importa la función createSlice, la acción getInitialPokeData y el tipo PokemonTypeInitialState. Luego, se define el estado inicial initialState con la propiedad allPokemon como undefined. A continuación, se crea el slice PokemonSlice utilizando createSlice, se define un extra reducer que se ejecuta cuando la acción getInitialPokeData.fulfilled ocurre y se exportan las acciones del slice.

    Este bloque de código define la acción asíncrona getPokeData utilizando createAsyncThunk.
    No se realiza ninguna acción dentro de la función getPokeData en este bloque en particular. 
    Solo se imprime un mensaje en la consola.
    Este bloque de código define la acción asíncrona getPokeData utilizando createAsyncThunk. 
    En este bloque en particular, no se ejecuta ninguna acción específica. Solo se muestra un 
    mensaje en la consola, pero esto se considera un efecto secundario y     no tiene un |
    impacto directo en el flujo de ejecución.
    Este bloque de código define la acción asíncrona getPokeData utilizando createAsyncThunk. 
    La acción recibe un array de genericPokemonType como parámetro y muestra por consola el array 
    en un bloque try-catch.

Glosario de términos:

    getPokeData: getPokeData es una acción asíncrona creada utilizando createAsyncThunk que se 
    utiliza para obtener datos aleatorios de pokémon. En este caso, la acción muestra por consola 
    el array de pokémons recibidos como parámetro.

    Bloque de código 4:

```typescript

import { createSlice } from "@reduxjs/toolkit";
import { PokemonTypeInitialState } from "../../utils/Types";
import { getInitialPokeData } from "../reducers/getInitialPokeData";


const initialState:PokemonTypeInitialState ={
    allPokemon: undefined,
};

export const PokemonSlice = createSlice({
    name:"pokemon",
    initialState, 
    reducers: {},
    extraReducers: (builder) => {
        builder.addCase(getInitialPokeData.fulfilled, (state,action)=>{
            state.allPokemon = action.payload
        });
    },
});

export const {} = PokemonSlice.actions;
```

En este bloque de código, se importa createSlice desde @reduxjs/toolkit, así como las interfaces y funciones necesarias.

Luego, se define una constante initialState que tiene el tipo PokemonTypeInitialState y se inicializa con un objeto que tiene una propiedad allPokemon establecida en undefined.

A continuación, se utiliza la función createSlice para crear un slice llamado "pokemon". Se especifica el initialState previamente definido, así como un objeto vacío para reducers y un objeto en extraReducers donde se define una acción getInitialPokeData.fulfilled que actualiza el estado allPokemon con el valor action.payload.

Finalmente, se exporta el slice PokemonSlice y se exportan las acciones (aunque en este caso no hay acciones definidas).

°Este bloque de código define el slice de Redux PokemonSlice utilizando createSlice. No se ejecuta ninguna acción directa en este bloque. Solo se define el slice y se agrega un caso adicional en extraReducers.

°Este bloque de código define la acción asíncrona getInitialPokeData utilizando createAsyncThunk y actualiza el estado allPokemon dentro del slice PokemonSlice en respuesta a laContinuación del bloque de código 6:acción asíncrona getInitialPokeData.fulfilled. 
°Este bloque de código importa la función createSlice, la acción getInitialPokeData y el tipo PokemonTypeInitialState. Luego, se define el estado inicial initialState con la propiedad allPokemon como undefined. A continuación, se crea el slice PokemonSlice utilizando createSlice, se define un extra reducer que se ejecuta cuando la acción getInitialPokeData.fulfilled ocurre y se exportan las acciones del slice.

Glosario de términos:

    createSlice: createSlice es una función de @reduxjs/toolkit que se utiliza para crear slices en Redux, que incluyen reducers y acciones relacionadas.
    extraReducers: extraReducerses una propiedad de createSlice que permite agregar reducers adicionales a un slice. Los extra reducers se ejecutan cuando se dispara una acción específica.
~~A continuación, se presenta un glosario de términos utilizados en este bloque:

Slice: En Redux, un slice es una porción del estado de la aplicación. Representa un conjunto específico de datos y las acciones relacionadas con esos datos. En este caso, el slice PokemonSlice representa el estado y las acciones relacionadas con los Pokémon.
   
Redux Toolkit: Redux Toolkit es una biblioteca oficial de Redux que proporciona una API simplificada para trabajar con Redux. Incluye funciones y utilidades para definir slices, acciones asíncronas y configurar la tienda de Redux de manera más sencilla.

Reducer: Un reducer es una función que especifica cómo se actualiza el estado de la aplicación en respuesta a una acción. En este bloque, el reducer se define utilizando el método createSlice y se pasa como parte de la configuración de PokemonSlice.

Action: En Redux, una acción es un objeto que describe un cambio en el estado de la aplicación. Puede contener datos adicionales que se utilizan para actualizar el estado. En este caso, la acción utilizada es getInitialPokeData.fulfilled, que se dispara cuando la acción asíncrona getInitialPokeData se completa exitosamente.

Extra Reducers: En Redux Toolkit, los extra reducers son bloques de código que se ejecutan en respuesta a acciones específicas. En este caso, se utiliza el método addCase para definir un extra reducer que se ejecutará cuando la acción getInitialPokeData.fulfilled ocurra. En este extra reducer, se actualiza el estado allPokemon con los datos obtenidos de la acción.

~~A continuación, se presenta un glosario de términos utilizados en este bloque:
Glosario de términos:

    createSlice: createSlice es una función de @reduxjs/toolkit que se utiliza para crear slices en Redux, que incluyen reducers y acciones relacionadas.
    extraReducers: extraReducerses una propiedad de createSlice que permite agregar reducers adicionales a un slice. Los extra reducers se ejecutan cuando se dispara una acción específica.
    Async Thunk: Un thunk asíncrono es una función que encapsula una operación asíncrona y se utiliza en Redux para manejar acciones asíncronas. En este bloque, se utiliza createAsyncThunk para crear la acción asíncrona getInitialPokeData.
    Fulfilled: En Redux Toolkit, fulfilled es un tipo de acción que se dispara cuando una acción asíncrona se completa exitosamente. En este bloque, se utiliza addCase para definir un extra reducer que se ejecuta cuando la acción getInitialPokeData.fulfilled ocurre.
    Extra Reducers: En Redux Toolkit, los extra reducers son bloques de código que se ejecutan en respuesta a acciones específicas. En este caso, se utiliza addCase para definir un extra reducer que actualiza el estado allPokemon dentro del slice PokemonSlice con los datos obtenidos de la acción.



    Bloque de código 5:

```typescript

import axios from 'axios';
import { createAsyncThunk } from "@reduxjs/toolkit";
import { pokemonsRoute } from '../../utils/Constants';

export const getInitialPokeData = createAsyncThunk("pokemon/initialData", async () => {
    try {
        const { data } = await axios.get(pokemonsRoute);
        console.log(data);
        return data.results;
    } catch (err) {
        console.log(err);
    }
});
```

En este bloque de código se define la acción asíncrona getInitialPokeData utilizando createAsyncThunk. Esta acción realiza una solicitud HTTP GET a la ruta pokemonsRoute utilizando axios y captura los datos de la respuesta en data. 

°Este bloque de código define la acción asíncrona getInitialPokeData utilizando createAsyncThunk. La acción que se realiza al ejecutarse es:

    Se realiza una solicitud HTTP GET utilizando axios.get a pokemonsRoute.
    Los datos de la respuesta se capturan en data.
    Se muestra data en la consola.
    Finalmente, se devuelve data.results.
°Este bloque de código importa la función createAsyncThunk, el tipo genericPokemonType y las constantes pokemonsRoute y axios. Luego, se define la acción asíncrona getInitialPokeData utilizando createAsyncThunk, que realiza una solicitud HTTP GET a la ruta pokemonsRoute y devuelve los resultados obtenidos.

Glosario de términos:

    createAsyncThunk: createAsyncThunk es una función de @reduxjs/toolkit que se utiliza para crear acciones asíncronas en Redux.
    axios: axios es una biblioteca popular de JavaScript utilizada para realizar solicitudes HTTP desde el navegador o desde Node.js.
    try-catch: try-catch es una estructura utilizada para capturar errores en JavaScript. En este caso, se utiliza para capturar cualquier error que ocurra durante la solicitud HTTP y se muestra en la consola.

A continuación, se presenta un glosario de términos utilizados en este bloque:

Axios: Axios es una biblioteca popular de JavaScript utilizada para realizar solicitudes HTTP desde el navegador o desde Node.js. En este bloque, se utiliza axios.get para realizar una solicitud HTTP GET a la ruta pokemonsRoute.

Async Thunk: Un thunk asíncrono es una función que encapsula una operación asíncrona y se utiliza en Redux para manejar acciones asíncronas. En este bloque, se utiliza createAsyncThunk para crear la acción asíncrona getInitialPokeData.

try-catch: El bloque try-catch es una estructura utilizada para capturar errores en JavaScript. En este bloque, se utiliza para capturar cualquier error que ocurra durante la solicitud HTTP y se muestra en la consola.

    Bloque de código 1:

```typescript

import { TypedUseSelectorHook, useDispatch, useSelector } from 'react-redux';
import type { RootState, AppDispatch } from './store';

// Use throughout your app instead of plain `useDispatch` and `useSelector`
export const useAppDispatch = () => useDispatch<AppDispatch>();
export const useAppSelector: TypedUseSelectorHook<RootState> = useSelector;
```

En este bloque de código se importan funciones y tipos de react-redux para su uso posterior. Luego, se definen dos funciones useAppDispatch y useAppSelector que se utilizan en toda la aplicación en lugar de utilizar useDispatch y useSelector directamente. Estas funciones están diseñadas para trabajar con los tipos de datos AppDispatch y RootState. 

°Este bloque de código importa funciones y tipos de react-redux. No realiza ninguna acción en sí mismo, solo importa las utilidades necesarias para su uso posterior.

A continuación, se presenta un glosario de términos utilizados en este bloque:
useDispatch: useDispatch es un hook de react-redux que se utiliza para obtener una instancia de la función dispatch de Redux en un componente de React. En este bloque, se utiliza para definir la función useAppDispatch, que devuelve una instancia tipada de useDispatch.

 useSelector: useSelector es un hook de react-redux que se utiliza para seleccionar una porción del estado de Redux en un componente de React. En este bloque, se utiliza para definir la función useAppSelector, que es una instancia tipada de useSelector que utiliza RootState.
RootState: El RootState es el tipo de dato que representa el estado raíz de la aplicación. En este bloque, se importa el tipo RootState desde el archivo store y se utiliza en useAppSelector para proporcionar un tipado específico al selector.

°Este bloque de código importa las funciones TypedUseSelectorHook, useDispatch y useSelector de react-redux y los tipos RootState y AppDispatch del archivo ./store. Luego, define las funciones useAppDispatch y useAppSelector que se utilizan en toda la aplicación. Estas funciones están diseñadas para trabajar con los tipos de datos AppDispatch y RootState.

Glosario de términos:

    TypedUseSelectorHook: TypedUseSelectorHook es un tipo definido por react-redux que permite utilizar un selector tipado en una función de componente de React.
    useDispatch: useDispatch es un hook de react-redux que se utiliza para obtener una instancia de la función dispatch de Redux en un componente de React.
    useSelector: useSelector es un hook de react-redux que se utiliza para seleccionar una porción del estado de Redux en un componente de React.
    RootState: RootState es el tipo de dato que representa el estado raíz de la aplicación.
    AppDispatch: AppDispatch es el tipo de dato que representa la función dispatch de la tienda de Redux.

Glosario de términos:

    Interface: En TypeScript, una interfaz es una forma de definir la estructura de un objeto. Permite definir los nombres de las propiedades y los tipos de datos que deben tener.
    Slice: En Redux, un slice es una porción del estado de la aplicación. Representa un conjunto específico de datos y las acciones relacionadas con esos datos.
    Redux Toolkit: Redux Toolkit es una biblioteca oficial de Reduxque proporciona una API simplificada para trabajar con Redux. Incluye funciones y utilidades para definir slices, acciones asíncronas y configurar la tienda de Redux de manera más sencilla.
    Reducer: Un reducer es una función que especifica cómo se actualiza el estado de la aplicación en respuesta a una acción.
    Action: En Redux, una acción es un objeto que describe un cambio en el estado de la aplicación.
    Dispatch: En Redux, dispatch es una función utilizada para enviar acciones a la tienda.
    Store: En Redux, la tienda (store) es el objeto central que contiene el estado de la aplicación.
    ThunkAction: ThunkAction es un tipo de dato utilizado en Redux para representar acciones asíncronas.
    Async Thunk: Un thunk asíncrono es una función que encapsula una operación asíncrona y se utiliza en Redux para manejar acciones asíncronas.
    Fulfilled: En Redux Toolkit, fulfilled es un tipo de acción que se dispara cuando una acción asíncrona se completa exitosamente.
    Axios: Axios es una biblioteca popular de JavaScript utilizada para realizar solicitudes HTTP desde el navegador o desde Node.js.
    Try-Catch: El bloque try-catch es una estructura utilizada para capturar errores en JavaScript.
    useDispatch: useDispatch es un hook de react-redux que se utiliza para obtener una instancia de la función dispatch de Redux en un componente de React.
    useSelector: useSelector es un hook de react-redux que se utiliza para seleccionar una porción del estado de Redux en un componente de React.
    RootState: El RootState es el tipo de dato que representa el estado raíz de la aplicación.

Espero que este glosario te ayude a comprender mejor los términos utilizados en la explicación de cada bloque de código.
