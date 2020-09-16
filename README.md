# ListagemCartao
ListagemDadosCliente.js

import React,{useState, useEffect} from 'react'
import {Text, View, Alert, Button} from 'react-native'
import ListaCartao from './ListaCartao'

export default function Lista (props){
    const id = props.route.params.idCliente
    const [data, setData] = useState([])
    const string = 'https://cartoes-piotto.herokuapp.com/api/cliente/'+id 
    
    useEffect(() => {
            fetch(string, {
            method: 'GET',
            headers: {
                'Accept' : 'application/json',
                'Authorization':'eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiIxNDg0ODY4MjAwMiIsInJvbGUiOiJST0xFX0VYQ0xVU0FPIiwiY3JlYXRlZCI6MTYwMDIwNzgyMzAzMCwiZXhwIjoxNjAwODEyNjIzfQ.FiXo232Ne42OG9C1EieP9GI9AQKqn5OnzFbrPjEnMZu16DtFEnPDbp-yWdAkBwf9zA9np4ivFI4GHN0911W8Lg'
            }
        })
        .then((response) => {   
            if(!response.ok){
                if(response.status == 400){
                    Alert.alert("Cliente nao encontrado!");
                    props.navigation.goBack()
                }
            }
            return response.json()
        })
        .then((json) => {
                setData(json.dados)
            }
        )
        .catch((error) => {
            console.error(error)})
        }, []);
    
    function renderizacao (){
        if(data != null){
            return (
                <>
                    <Text style={{fontSize:24, color:'blue', fontWeight:'bold'}}>
                        Cliente  
                    </Text>
                    <Text>
                        ID: {data.id}
                    </Text>
                    <Text>
                        CPF: {data.cpf} 
                    </Text>
                    <Text>
                        Nome: {data.nome}
                    </Text>
                    <Text>
                        UF: {data.uf}
                    </Text>
                    <Button title="Voltar" onPress={() => props.navigation.goBack()}/>  
                    <Button title="Listar cartoes" onPress={ListaCartao} />
                </>
            )
        }
    }

    return(
        <View style={{flex:1, padding: 24}}>
            {renderizacao()}
        </View>
    );
}


ListaCartao.js

import React,{useState, useEffect} from 'react'
import {Text, View, Alert, Button} from 'react-native'

export default function Lista (props){
    const id = props.route.params.idCliente
    const [data, setData] = useState([])
    const string = 'https://cartoes-piotto.herokuapp.com/api/cartao/'+id 
    
    useEffect(() => {
            fetch(string, {
            method: 'GET',
            headers: {
                'Accept' : 'application/json',
                'Authorization':'eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiIxNDg0ODY4MjAwMiIsInJvbGUiOiJST0xFX0VYQ0xVU0FPIiwiY3JlYXRlZCI6MTYwMDIwNzgyMzAzMCwiZXhwIjoxNjAwODEyNjIzfQ.FiXo232Ne42OG9C1EieP9GI9AQKqn5OnzFbrPjEnMZu16DtFEnPDbp-yWdAkBwf9zA9np4ivFI4GHN0911W8Lg'
            }
        })
        .then((response) => {   
            if(!response.ok){
                if(response.status == 400){
                    Alert.alert("Cartão nao encontrado!");
                    props.navigation.goBack()
                }
            }
            return response.json()
        })
        .then((json) => {
                setData(json.dados)
            }
        )
        .catch((error) => {
            console.error(error)})
        }, []);
    
    function renderizacao (){
        if(data != null){
            return (
                <>
                    <Text style={{fontSize:24, color:'blue', fontWeight:'bold'}}>
                        Cartao  
                    </Text>
                    <Text>
                        ID: {data.id}
                    </Text>
                    <Text>
                        Numero: {data.numero} 
                    </Text>
                    <Text>
                        dataValidade: {data.datavalidade}
                    </Text>
                    <Text>
                        clientId: {data.idCliente}
                    </Text>
                    <Button title="Voltar" onPress={() => props.navigation.goBack()}/>  
                </>
            )
        }
    }

    return(
        <View style={{flex:1, padding: 24}}>
            {renderizacao()}
        </View>
    );
}
