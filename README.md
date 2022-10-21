MongoDB

comandos

Notas:
-Mongo NO tiene estructura de una tabla como base de datos relacionales
-NameCollection = Es una variable en el texto, aquí va el nombre de la colección
-NameDB = Es una variable en el texto, aquí va el nombre de la Base de datos
-cuando se guarda una colección se genera un id, eso es por parte de mongodb
-mongodb modifica los datos para que el los entienda, por ejemplo el new date
- se pueden guardar listas e incluso objetos dentro del objetos

"Base de datos"

-ver base de datos: show dbs
-usar/crear una base de datos: use NameDB
#Sí se crea una base de datos, pero no se genera ninguna colección dentro de ella, no se guarda#
-ver la base de datos actual: db
-eliminar base de datos: db.dropDatabase()
#Se elimina la base de datos que se este usando, por eso siempre es recomendable ver cual es la base de datos actual


"Colecciones"

-ver las colecciones: show collections
-crear una colección: db.CreateCollection("NameCollection")
#tambien se pueden crear un colección insertando un documentos en una colección que no existe, MongoDB va a crear la colección por ti
-eliminar colecciones: db.NameCollection.drop()

                                

                              ===Documentos===


$insertar$

-crear un documentos: db.NameCollection.insert({"nombre":"algo"})
#se puede insertar un dato en una colección que no existe, MongoDB va a crear la colección por nosotros
-ver documentos dentro de las colecciones: db.NameCollection.find()
-ver documentos dentro de las colecciones BONITO: db.NameCollection.find().pretty()
-guardar varias documentos a la vez:
#se puede guardar varias documentos a la vez, en un lugar de pasarle un objeot se puede pasar una lista de objetos


$Buscar$

Buscar documento: db.NameCollection.find({"algo":"algo"})
#se pueden meter mas filtros por ejemplo db.NameCollection.find({"algo":"algo","algo2":"algo2","algo3":"algo3"})
BUscar documentos PERO devuelve solo uno: db.NameCollection.finOne({"algo":"algo"})#te devuelve el primero 
BUscar un documento PERO muestra datos especificos del objetos:db.NameCollection.find({"algo":"algo"},{"name":1,"descripcion":1,"_id":0})
Ordenar los resultados de la busqueda de documentos: db.NameCollection.fin({"algo":"algo"}).sort({"name":1})
limitar el numero de resultado: db.NameCollection.find({"algo":"algo"}).limit(2)
contar cuantos documentos hay en una colección: db.NameCollection.count()
#el comando sirve, pero es mas actaul db.NameCollection.countDocuments()
funciones en documentos: db.NameCollection.find().forEach(productos=>print("Productos: "+ productos.nombre))

$Actualizar$

Actualizar un objetos: db.NameCollection.update({"algo":"algo"},{$set:{"algo"}:{"algo"}})
#la funcion update recibe dos objetos, el primero es el filtro de busqueda y el seguno es la nueva informacion
Insertar un objeto si no hay coincidencias: db.NameCollection.update({"algo":"algo"},{$set:{"algo":"algo"}},upsert:ture)
Incrementar datos numeros : db.NameDocument.update({"algo":"algo"},{$inc:{"algo":0.1}})
Renombrar un valor del documento: db.NameCollection.update({"algo":"algo"},{$rename:{"algo":"algo"}}) 
#a diferencia del $set, el $rename cambiar el titolo de la propiedad no el atributo

$ELiminar$

eliminar un documenot db.NameCollection.remove({"algo":"algo"})
#los parametros que recibe son para la busqueda del elemento a eliminar y aunque funciona el comando es mas nuevo el removeOne, removeMany
para eliminar todos los documentos a la vez: db.NameCollection.remove({})

para crear un backup de nuestra base de datos es:

mongodump

para restaurar: 

mongorestore




ejemplo para insertar varios:

db.productos.insert([
    {
        "nombre":"mouse",
        "descripcions":"gamer",
        "tags":["gamer","computers"],
        "cantidad":12,
        "fechaCreacion": new Date()        
    },
    {
        "nombre":"monitor",
        "descripcions":"lg monitos",
        "tags":["gamer","computers"],
        "cantidad":1,
        "fechaCreacion": new Date()        
    },
    {
        "nombre":"teclado",
        "descripcions":"gamer",
        "tags":["gamer","computers"],
        "cantidad":2,
        "fechaCreacion": new Date()        
    }
    
])
