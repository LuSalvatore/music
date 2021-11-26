# music
App de Música onepage para Android.
//This Code no it Html > Não é um codigo para site mas sim um codigo de um app de Musica, feito em react native ;)
//////////////////////////////////////////////////////////////////////////////////////////////////////////////////
//////////////////////////////////////////////////////////////////////////////////////////////////////////////////
//////////////////////////////////////////////////////////////////////////////////////////////////////////////////
import { StatusBar } from 'expo-status-bar';
import React, { useState } from 'react';
import {audio} from 'expo-av';
import {AntDesign} from '@expo/vector-icons';
import { LogBox, ScrollView, StyleSheet, Text, TouchableOpacity, View } from 'react-native';


export default function App() {
///////////////////////////////////////////////////////////////////////////////////////////////////
//const, var, if and else

LogBox.ignoreAllLogs(true);

const [audioIndex, setaraudioIndex] = useState(0);
const [playing, setarplaying] = useState(false);
const [audio, setarAudio] = useState (null);
const {musicas, setarMusicas} = useState ([

  { nome:'Chefão', artista:'Aguia', playing:false, file: '' },

  { nome:'Falcão', artista:'Aguia', playing:false, file: '' },
  
  { nome:'100%', artista:'Aguia', playing:false, file: require('./audio.mp3') },
]);
const changeMusic = async (id) =>{
  let curFile = null;
  let newMusics = musicas.filter((val,k)=> {
  
    if(id == k){musicas[k].playing = true;
    curFile = musicas[k].file;
    setarplaying(true);
    setaraudioIndex(id);

  }else{musicas[k].playing = false;
    }
    
  return musicas[k];
  })

  if(audio != null){
    audio.unloadAsync();
  }

  let urAudio = new Audio.sound();

  try{
    await curAudio.loadAsync(curFile);
    await curAudio.playAsync();
  }catch(error){}


  setarAudio(curAudio);
  setarMusicas(newMusics);

const handleplay = async()=>{
  let curFile = musicas[audioIndex].file;
  let newMusics = musicas.filter((val,k)=> {
  
    if(audioIndex == k){musicas[k].playing = true;
    curFile = musicas[k].file;
   

  }else{musicas[k].playing = false;
    }
    
  return musicas[k];
  })
  try{
    if(audio != null){
      setarplaying(true);
      setarMusicas(newMusics);
      await audio.playAsync();
    }else{
      let curAudio = new Audio.Sound();
      try{
        await curAudio.loadAsync(curAudio);
        await curAudio.playAsync();
      }catch(error){}
      setarAudio(curAudio);
      setarMusicas(newMusics);
      setarplaying(true);
    }
  }catch(error){}
}
const handlepause = async()=>{
  if(audio!=null){
    audio.pauseAsync();
  }
  setarplaying(false);
}
}

///////////////////////////////////////////////////////////////////////////////////////////////////
  return (
    <View style={{flex:1}}>
      <ScrollView style={style.container}>
        <StatusBar hidden />
          <View>
            <Text style={style.textheader}> Musicas para Drop | Salvatore Media</Text>
          </View>

          <View style={style.table}>
            <Text style={{width:'50%', color:'rgb(200,200,200)'}}>MÚSICA</Text>
            <Text style={{width:'50%', color:'rgb(200,200,200)'}}>ARTISTA</Text>
          </View>

          {
            musicas.map((val,K)=>{
              if(Val.playing){
                return(
                <View style={style.tale}>
                  <TouchableOpacity onPress={()=>changeMusic(k)} style={{width:'100%', flexDirection:'row'}}>
                    <Text style={{width:'50%', color:'1DB954'}}> <AntDesign namme="Play" size={15}/> {val.nome} </Text>
                    <Text style={{width:'50%', color:'white'}}>{val.artista}</Text>
                  </TouchableOpacity>
                </View>
            );
              }else{
                return(
                  <View style={style.tale}>
                    <TouchableOpacity  onPress={()=>changeMusic(k)} style={{width:'100%', flexDirection:'row'}}>
                      <Text style={{width:'50%', color:'white'}}> <AntDesign namme="Play" size={15}/> {val.nome} </Text>
                      <Text style={{width:'50%', color:'white'}}>{val.artista}</Text>
                    </TouchableOpacity>
                  </View>
              );
              }})}
               <View style={{paddingBottom:200}}></View>
      </ScrollView>
      <View style={style.player}>
      <TouchableOpacity style={{marginRight:20,marginLeft:20}}>
        <AntDesign name="banckward" size={35} color='white' />
      </TouchableOpacity>
      {
        (!playing)?
      <TouchableOpacity onPress={()=> handleplay()} style={{marginRight:20,marginLeft:20}}>
        <AntDesign name="playcircleo" size={35} color='white' />
      </TouchableOpacity>
      :
      <TouchableOpacity onPress={()=> handlepause()} style={{marginRight:20,marginLeft:20}}>
      <AntDesign name="pausecircleo" size={35} color='white' />
    </TouchableOpacity>
      }
      <TouchableOpacity style={{marginRight:20,marginLeft:20}}>
        <AntDesign name="forward" size={35} color='white' />
      </TouchableOpacity>
      </View>
      </View>
  );
}



///////////////////////////////////////////////////////////////////////////////////////////////////
const styles = StyleSheet.create({
  
  
  boxnumber:{padding:10, borderBottomColor:'black', borderBottomWidth:2},

  player:{width:'100%', height:100, position:'absolute', bottom:0, left:0, zIndex:999, backgroundColor:'#111', alignItems:'center', justifyContent:'center', flexDirection:'row'},

  container:{flex:1, backgroundColor:'#222'},

  table:{flexDirection:'row', padding:20, borderBottomColor:'white', borderBottomWidth:1},

  textheader:{textAlign:'center', color:'White', fontSize:20, marginTop:22},
  
  coverView:{width:'100%', height:80, backgroundColor:'rgba(0,0,0,0.5)'},
  
  image:{width:'100%', height:100, resizeMode:"cover", justifyContent:'center'},
    
  Adicionar:{width:200, padding:8, backgroundColor:'Yellow', marginTop:20},
  
  botões:{width:'25%', backgroundColor:'black', justifyContent:'center', alignItems:'center', height:'100%'},
  
  header:{width:'100%',padding:20,backgroundColor:'#1DB954'},
  
  anotação:{fontSize:14},
  
  botãoprincipal:{position:'absolute',right:20,bottom:20,width:50,height:50,backgroundColor:'#069',borderRadius:25},
  
  oxdobotão:{color:'White',position:'relative',textAlign:'center',top:3,fontSize:30},
  
  botãosalvo:{position:'absolute',right:20,bottom:20,width:50,paddingTop:10,paddingBottom:10,backgroundColor:'#069',borderRadius:10},
  
  centeredView: {flex: 1,justifyContent: 'center',alignItems: 'center',marginTop: 22},
  
  modalView: {margin: 20,backgroundColor: 'white',borderRadius: 20,padding: 35,alignItems: 'center',shadowColor: '#000',shadowOpacity: 0.25,shadowRadius: 4,elevation: 5},
  
  shadowOffset: {width: 0,height: 2},
  
  button: {borderRadius: 20,padding: 10,elevation: 2},
  
  buttonOpen: {backgroundColor: '#F194FF'},
  
  buttonClose: {backgroundColor: '#2196F3'},
  
  textStyle: {color: 'white',fontWeight: 'bold',textAlign: 'center'},
  
  modalText: {marginBottom: 15,textAlign: 'center'},

});
