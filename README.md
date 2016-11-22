## RESTful ##
En una **API RESTful** se emplean todos los verbos HTTP (GET, POST, PUT y DELETE principalmente). Nos permite:

Listar colección | GET | http://localhost/api/:coleccion

Obtener un documento de la colección | GET | http://localhost/api/:coleccion/:id

Insertar un documento en la colección | POST | http://localhost/api/:coleccion

Actualizar un documento | PUT |  http://localhost/api/:coleccion/:id

Eliminar un documento | DELETE | http://localhost/api/:coleccion/:id

En comparacion con una aplicación **CRUD** (Create/Read/Update/Delete) utiliza todos los verbos HTTP.    



El servicio RESTful contiene los siguientes atributos:

host: URL del host donde se ubica el servicio web a invocar. Para este atributo se utilizará la varible global host.

port: Puerto por el que está escuchando el servicio web a invocar. El valor de este atributo será la el de la variable globar port.

path: Ruta de la aplicación web utilizada para el servicio web. Se utilizará la varible path definida anteriomente para definir el valor de este atributo.

method: Método o verbo HTTP RESTful (GET, POST, PUT o DELETE) utilizado en este servicio web. Para la carga de usuarios se utilizará el método GET.

encoding: Define la codificación de la petición al servicio web. En este caso no hay ninguna codificación por lo que se configura a null.

Un servicio RESTful se construye de la siguiente manera, basandonos en el patron MVC:


* Construimos el modelo. Tomaremos como ejemplo el siguiente esquema: models/tvshow.js

  var mongoose = require('mongoose'),  
  Schema   = mongoose.Schema;

  var tvshowSchema = new Schema({  
  title:    { type: String },
  year:     { type: Number },
  country:  { type: String },
  poster:   { type: String },
  seasons:  { type: Number },
  genre:    { type: String, enum:
  ['Drama', 'Fantasy', 'Sci-Fi', 'Thriller', 'Comedy']
        },
  summary:  { type: String }
});

module.exports = mongoose.model('TVShow', tvshowSchema);  

* Construimos el controlador en el cual haremos las funciones POST, PUT, GET o DELETE. En el siguiente fragmento se muestra el GET:
  //GET - Return a TVShow with specified ID
    exports.findById = function(req, res) {  
    TVShow.findById(req.params.id, function(err, tvshow) {
    if(err) return res.send(500. err.message);

    console.log('GET /tvshow/' + req.params.id);
        res.status(200).jsonp(tvshow);
    });
};



  //DELETE - Delete a TVShow with specified ID
    exports.deleteTVShow = function(req, res) {  
    TVShow.findById(req.params.id, function(err, tvshow) {
        tvshow.remove(function(err) {
            if(err) return res.status(500).send(err.message);
      res.status(200).send();
        })
    });
};


* Construir la vista para mostrar datos o mensajes de Error.

