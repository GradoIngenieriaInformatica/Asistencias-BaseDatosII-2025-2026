# Asistencia Samuel Herrera
BANCO DE RESPUESTAS CONFIGURADO - NoSQL (MONGODB Y NEO4J)
================================================================================

--------------------------------------------------------------------------------
SECCIÓN 1: CONSULTAS EXCLUSIVAS DE MONGODB (Universidad Mongo)
--------------------------------------------------------------------------------

IDENTIFICADOR: PREGUNTA MONGO 1
NIVEL: Fácil
ENUNCIADO: Buscar usuarios que sean mayores de 18 años y que estén activos.
SINTAXIS REQUERIDA:
db.usuarios.find({ edad: { $gt: 18 }, estado: "activo" })

--------------------------------------------------------------------------------

IDENTIFICADOR: PREGUNTA MONGO 2
NIVEL: Fácil
ENUNCIADO: Buscar productos que tengan un precio entre 40 y 200 dólares.
SINTAXIS REQUERIDA:
db.productos.find({ precio: { $gte: 40, $lte: 200 } })

--------------------------------------------------------------------------------

IDENTIFICADOR: PREGUNTA MONGO 3
NIVEL: Medio
ENUNCIADO: Buscar usuarios que sepan usar la tecnología "mongodb".
SINTAXIS REQUERIDA:
db.usuarios.find({ tecnologias: "mongodb" })

--------------------------------------------------------------------------------

IDENTIFICADOR: PREGUNTA MONGO 4
NIVEL: Difícil (Framework de Agregación)
ENUNCIADO: Calcular el total de dinero vendido por cada Categoría usando la colección de ventas.
SINTAXIS REQUERIDA:
db.ventas.aggregate([
{ $group: { _id: "$categoria", totalVendido: { $sum: "$monto" }, cantidadVentas: { $sum: 1 } } }
])

--------------------------------------------------------------------------------

IDENTIFICADOR: PREGUNTA MONGO 5
NIVEL: Difícil (Simulación de JOIN Relacional)
ENUNCIADO: Simular un 'JOIN' de SQL para unir la colección de Empleados con sus Departamentos.
SINTAXIS REQUERIDA:
db.empleados.aggregate([
{ $lookup: { from: "departamentos", localField: "departamentoId", foreignField: "_id", as: "info_departamento" } }
])


--------------------------------------------------------------------------------
SECCIÓN 2: BANCO OFICIAL DE 100 EJERCICIOS DE NEO4J (Cypher)
--------------------------------------------------------------------------------

IDENTIFICADOR: ID 1
NIVEL: facil
ENUNCIADO: Obtén todas las personas que trabajan en alguna empresa y muestra el nombre de la persona y de la empresa.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:TRABAJA_EN]->(e:Empresa)
RETURN p.nombre, e.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 2
NIVEL: facil
ENUNCIADO: Lista todas las personas que viven en Madrid.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:VIVE_EN]->(c:Ciudad {nombre:'Madrid'})
RETURN p.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 3
NIVEL: facil
ENUNCIADO: Corrige la consulta para devolver correctamente nombres de personas.
SINTAXIS REQUERIDA:
MATCH (p:Persona)
RETURN p.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 4
NIVEL: facil
ENUNCIADO: Modifica la consulta para limitar a 2 resultados.
SINTAXIS REQUERIDA:
MATCH (p:Persona)
RETURN p.nombre
LIMIT 2

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 5
NIVEL: medio
ENUNCIADO: Obtén las empresas junto con el número de empleados.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:TRABAJA_EN]->(e:Empresa)
RETURN e.nombre, count(p)

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 6
NIVEL: medio
ENUNCIADO: Encuentra personas que participan en proyectos y trabajan en empresa.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:TRABAJA_EN]->(e:Empresa), (p)-[:PARTICIPA_EN]->(pr:Proyecto)
RETURN p.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 7
NIVEL: medio
ENUNCIADO: Corrige la consulta para usar WHERE correctamente.
SINTAXIS REQUERIDA:
MATCH (p:Persona)
WHERE p.nombre='Ana'
RETURN p

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 8
NIVEL: medio
ENUNCIADO: Modifica la consulta para ordenar por nombre.
SINTAXIS REQUERIDA:
MATCH (p:Persona)
RETURN p.nombre
ORDER BY p.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 9
NIVEL: medio
ENUNCIADO: Encuentra personas con al menos 2 amigos.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:AMIGO_DE]->(a:Persona)
WITH p, count(a) as amigos
WHERE amigos >= 2
RETURN p.nombre, amigos

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 10
NIVEL: dificil
ENUNCIADO: Encuentra caminos de longitud hasta 2 entre personas.
SINTAXIS REQUERIDA:
MATCH p=(a:Persona)-[:AMIGO_DE*1..2]->(b:Persona)
RETURN p

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 11
NIVEL: dificil
ENUNCIADO: Encuentra personas conectados a proyectos a través de amigos.
SINTAXIS REQUERIDA:
MATCH (a:Persona)-[:AMIGO_DE]->(b:Persona)-[:PARTICIPA_EN]->(pr:Proyecto)
RETURN a.nombre, pr.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 12
NIVEL: dificil
ENUNCIADO: Corrige la consulta para usar length correctamente.
SINTAXIS REQUERIDA:
MATCH p=(a)-[:AMIGO_DE*]->(b)
RETURN length(p)

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 13
NIVEL: dificil
ENUNCIADO: Modifica la consulta para devolver solo la longitud del path.
SINTAXIS REQUERIDA:
MATCH p=(a:Persona)-[:AMIGO_DE*1..3]->(b:Persona)
RETURN length(p)

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 14
NIVEL: medio
ENUNCIADO: Encuentra personas que no participan en proyectos.
SINTAXIS REQUERIDA:
MATCH (p:Persona)
OPTIONAL MATCH (p)-[:PARTICIPA_EN]->(pr)
WHERE pr IS NULL
RETURN p.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 15
NIVEL: dificil
ENUNCIADO: Encuentra personas que actúan como puente en relaciones de amistad.
SINTAXIS REQUERIDA:
MATCH (a:Persona)-[:AMIGO_DE]->(b:Persona)-[:AMIGO_DE]->(c:Persona)
RETURN b, count(*)

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 16
NIVEL: medio
ENUNCIADO: Obtén todas las personas junto con la ciudad en la que viven.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:VIVE_EN]->(c:Ciudad)
RETURN p.nombre, c.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 17
NIVEL: medio
ENUNCIADO: Cuenta cuántas personas viven en cada ciudad.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:VIVE_EN]->(c:Ciudad)
RETURN c.nombre, count(p)

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 18
NIVEL: medio
ENUNCIADO: Modifica la consulta para devolver solo las ciudades con más de 2 personas.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:VIVE_EN]->(c:Ciudad)
WITH c, count(p) as total
WHERE total > 2
RETURN c.nombre, total

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 19
NIVEL: medio
ENUNCIADO: Corrige la consulta para que agrupe correctamente.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:TRABAJA_EN]->(e:Empresa)
RETURN e.nombre, count(p)

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 20
NIVEL: medio
ENUNCIADO: Obtén personas junto con el número de tecnologías que usan.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:USA_TECNOLOGIA]->(t:Tecnologia)
RETURN p.nombre, count(t)

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 21
NIVEL: medio
ENUNCIADO: Encuentra personas que usan la tecnología Neo4j.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:USA_TECNOLOGIA]->(t:Tecnologia {nombre:'Neo4j'})
RETURN p.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 22
NIVEL: medio
ENUNCIADO: Encuentra personas que trabajan en la misma empresa.
SINTAXIS REQUERIDA:
MATCH (p1:Persona)-[:TRABAJA_EN]->(e:Empresa)<-[:TRABAJA_EN]-(p2:Persona)
WHERE p1 <> p2
RETURN p1.nombre, p2.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 23
NIVEL: medio
ENUNCIADO: Modifica la consulta para evitar duplicados en pares de personas.
SINTAXIS REQUERIDA:
MATCH (p1:Persona)-[:TRABAJA_EN]->(e)<-[:TRABAJA_EN]-(p2:Persona)
WHERE id(p1) < id(p2)
RETURN p1.nombre, p2.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 24
NIVEL: medio
ENUNCIADO: Obtén proyectos junto con el total de horas invertidas por personas.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[r:PARTICIPA_EN]->(pr:Proyecto)
RETURN pr.nombre, sum(r.horas)

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 25
NIVEL: medio
ENUNCIADO: Corrige la consulta para usar propiedades de relación.
SINTAXIS REQUERIDA:
MATCH (p)-[r:PARTICIPA_EN]->(pr)
RETURN pr.nombre, sum(r.horas)

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 26
NIVEL: dificil
ENUNCIADO: Encuentra personas conectadas por cadenas de amistad de hasta longitud 3.
SINTAXIS REQUERIDA:
MATCH (a:Persona)-[:AMIGO_DE*1..3]->(b:Persona)
RETURN a.nombre, b.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 27
NIVEL: dificil
ENUNCIADO: Devuelve los paths de amistad junto con su longitud.
SINTAXIS REQUERIDA:
MATCH p=(a:Persona)-[:AMIGO_DE*1..3]->(b:Persona)
RETURN p, length(p)

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 28
NIVEL: dificil
ENUNCIADO: Modifica la consulta para devolver solo paths de longitud mayor a 1.
SINTAXIS REQUERIDA:
MATCH p=(a:Persona)-[:AMIGO_DE*1..3]->(b:Persona)
WHERE length(p) > 1
RETURN p

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 29
NIVEL: dificil
ENUNCIADO: Obtén los nodos intermedios en paths de amistad.
SINTAXIS REQUERIDA:
MATCH p=(a:Persona)-[:AMIGO_DE*2..3]->(b:Persona)
RETURN nodes(p)

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 30
NIVEL: dificil
ENUNCIADO: Obtén las relaciones de un path.
SINTAXIS REQUERIDA:
MATCH p=(a:Persona)-[:AMIGO_DE*1..3]->(b:Persona)
RETURN relationships(p)

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 31
NIVEL: medio
ENUNCIADO: Obtén personas junto con la universidad en la que estudiaron.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:ESTUDIO_EN]->(u:Universidad)
RETURN p.nombre, u.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 32
NIVEL: medio
ENUNCIADO: Encuentra universidades con más de un estudiante.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:ESTUDIO_EN]->(u:Universidad)
WITH u, count(p) as total
WHERE total > 1
RETURN u.nombre, total

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 33
NIVEL: medio
ENUNCIADO: Corrige la consulta para usar WITH correctamente.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:VIVE_EN]->(c)
RETURN c

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 34
NIVEL: medio
ENUNCIADO: Modifica la consulta para devolver solo ciudades únicas.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:VIVE_EN]->(c:Ciudad)
RETURN DISTINCT c.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 35
NIVEL: dificil
ENUNCIADO: Encuentra personas que trabajan con alguien que usa Neo4j.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:TRABAJA_CON]->(o:Persona)-[:USA_TECNOLOGIA]->(t:Tecnologia {nombre:'Neo4j'})
RETURN p.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 36
NIVEL: dificil
ENUNCIADO: Encuentra personas que viven en una ciudad distinta a la de sus amigos.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:AMIGO_DE]->(a:Persona),(p)-[:VIVE_EN]->(c1),(a)-[:VIVE_EN]->(c2)
WHERE c1 <> c2
RETURN p.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 37
NIVEL: dificil
ENUNCIADO: Encuentra personas que gestionan proyectos en los que no participan.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:GESTIONA]->(pr:Proyecto)
WHERE NOT (p)-[:PARTICIPA_EN]->(pr)
RETURN p.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 38
NIVEL: medio
ENUNCIADO: Obtén personas junto con el número de amigos.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:AMIGO_DE]->(a:Persona)
RETURN p.nombre, count(a)

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 39
NIVEL: medio
ENUNCIADO: Modifica la consulta para mostrar solo personas con más de un amigo.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:AMIGO_DE]->(a:Persona)
WITH p, count(a) as total
WHERE total > 1
RETURN p.nombre, total

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 40
NIVEL: dificil
ENUNCIADO: Encuentra caminos entre personas donde todas las relaciones tienen propiedad since > 2018.
SINTAXIS REQUERIDA:
MATCH p=(a:Persona)-[:AMIGO_DE*]->(b:Persona)
WHERE ALL(r IN relationships(p) WHERE r.since > 2018)
RETURN p

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 41
NIVEL: medio
ENUNCIADO: Obtén personas junto con el número de proyectos en los que participan.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:PARTICIPA_EN]->(pr:Proyecto)
RETURN p.nombre, count(pr)

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 42
NIVEL: medio
ENUNCIADO: Modifica la consulta para incluir también personas sin proyectos.
SINTAXIS REQUERIDA:
MATCH (p:Persona)
OPTIONAL MATCH (p)-[:PARTICIPA_EN]->(pr:Proyecto)
RETURN p.nombre, count(pr)

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 43
NIVEL: medio
ENUNCIADO: Encuentra personas que participan en más de un proyecto.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:PARTICIPA_EN]->(pr:Proyecto)
WITH p, count(pr) as total
WHERE total > 1
RETURN p.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 44
NIVEL: medio
ENUNCIADO: Obtén proyectos junto con el número de personas distintas que participan en ellos.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:PARTICIPA_EN]->(pr:Proyecto)
RETURN pr.nombre, count(DISTINCT p)

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 45
NIVEL: medio
ENUNCIADO: Corrige la consulta para evitar duplicados en el conteo.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:PARTICIPA_EN]->(pr:Proyecto)
RETURN pr.nombre, count(DISTINCT p)

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 46
NIVEL: dificil
ENUNCIADO: Encuentra personas que trabajan en empresas donde al menos uno de sus compañeros usa Neo4j.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:TRABAJA_EN]->(e:Empresa)<-[:TRABAJA_EN]-(o:Persona)-[:USA_TECNOLOGIA]->(t:Tecnologia {nombre:'Neo4j'})
RETURN DISTINCT p.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 47
NIVEL: dificil
ENUNCIADO: Encuentra personas que tienen amigos que trabajan en una empresa distinta a la suya.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:TRABAJA_EN]->(e1:Empresa),(p)-[:AMIGO_DE]->(a:Persona)-[:TRABAJA_EN]->(e2:Empresa)
WHERE e1 <> e2
RETURN p.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 48
NIVEL: dificil
ENUNCIADO: Encuentra pares de personas que viven in la misma ciudad y trabajan juntas.
SINTAXIS REQUERIDA:
MATCH (p1:Persona)-[:TRABAJA_CON]->(p2:Persona),(p1)-[:VIVE_EN]->(c),(p2)-[:VIVE_EN]->(c)
RETURN p1.nombre, p2.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 49
NIVEL: dificil
ENUNCIADO: Modifica la consulta para evitar pares duplicados.
SINTAXIS REQUERIDA:
MATCH (p1:Persona)-[:TRABAJA_CON]->(p2:Persona)
WHERE id(p1) < id(p2)
RETURN p1.nombre, p2.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 50
NIVEL: dificil
ENUNCIADO: Encuentra personas que están conectadas por amistad a alguien que participa en más de un proyecto.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:AMIGO_DE]->(a:Persona)-[:PARTICIPA_EN]->(pr:Proyecto)
WITH a, count(pr) as total, p
WHERE total > 1
RETURN p.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 51
NIVEL: dificil
ENUNCIADO: Encuentra personas que usan exactamente una tecnología.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:USA_TECNOLOGIA]->(t:Tecnologia)
WITH p, count(t) as total
WHERE total = 1
RETURN p.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 52
NIVEL: dificil
ENUNCIADO: Encuentra personas que no tienen amigos.
SINTAXIS REQUERIDA:
MATCH (p:Persona)
WHERE NOT (p)-[:AMIGO_DE]->()
RETURN p.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 53
NIVEL: dificil
ENUNCIADO: Corrige la consulta para usar OPTIONAL MATCH correctamente.
SINTAXIS REQUERIDA:
MATCH (p:Persona)
OPTIONAL MATCH (p)-[:PARTICIPA_EN]->(pr)
RETURN p, pr

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 54
NIVEL: dificil
ENUNCIADO: Encuentra caminos de amistad donde todos los nodos intermedios viven en la misma ciudad.
SINTAXIS REQUERIDA:
MATCH p=(a:Persona)-[:AMIGO_DE*2..3]->(b:Persona)
WHERE ALL(n IN nodes(p)[1..-1] WHERE (n)-[:VIVE_EN]->(:Ciudad))
RETURN p

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 55
NIVEL: dificil
ENUNCIADO: Encuentra personas que aparecen en más de un path de amistad.
SINTAXIS REQUERIDA:
MATCH p=(a:Persona)-[:AMIGO_DE*1..3]->(b:Persona)
UNWIND nodes(p) as n
WITH n, count(*) as total
WHERE total > 1
RETURN n, total

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 56
NIVEL: medio
ENUNCIADO: Obtén personas junto con todas las tecnologías que usan.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:USA_TECNOLOGIA]->(t:Tecnologia)
RETURN p.nombre, collect(t.nombre)

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 57
NIVEL: medio
ENUNCIADO: Modifica la consulta para devolver solo personas que usan más de una tecnología.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:USA_TECNOLOGIA]->(t:Tecnologia)
WITH p, collect(t) as techs
WHERE size(techs) > 1
RETURN p.nombre, techs

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 58
NIVEL: dificil
ENUNCIADO: Encuentra tecnologías usadas por personas que trabajan en TechCorp.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:TRABAJA_EN]->(:Empresa {nombre:'TechCorp'}),(p)-[:USA_TECNOLOGIA]->(t:Tecnologia)
RETURN DISTINCT t.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 59
NIVEL: dificil
ENUNCIADO: Encuentra personas que trabajan en todas las empresas presentes en el grafo.
SINTAXIS REQUERIDA:
MATCH (e:Empresa)
WITH count(e) as total
MATCH (p:Persona)-[:TRABAJA_EN]->(e:Empresa)
WITH p, count(DISTINCT e) as c, total
WHERE c = total
RETURN p.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 60
NIVEL: dificil
ENUNCIADO: Encuentra personas que comparten todas sus tecnologías con al menos otra persona.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:USA_TECNOLOGIA]->(t:Tecnologia)
WITH p, collect(t) as techs
MATCH (o:Persona)-[:USA_TECNOLOGIA]->(t2:Tecnologia)
WITH p, techs, o, collect(t2) as techs2
WHERE techs = techs2 AND p <> o
RETURN p.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 61
NIVEL: dificil
ENUNCIADO: Corrige la consulta para usar correctamente UNWIND.
SINTAXIS REQUERIDA:
MATCH p=(a)-[:AMIGO_DE*]->(b)
UNWIND nodes(p) as n
RETURN n

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 62
NIVEL: dificil
ENUNCIADO: Modifica la consulta para contar cuántas veces aparece cada nodo en paths.
SINTAXIS REQUERIDA:
MATCH p=(a)-[:AMIGO_DE*]->(b)
UNWIND nodes(p) as n
RETURN n, count(*)

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 63
NIVEL: dificil
ENUNCIADO: Encuentra personas que están conectadas a todas las demás mediante algún path.
SINTAXIS REQUERIDA:
MATCH (p:Persona)
MATCH (p)-[:AMIGO_DE*]->(o:Persona)
WITH p, count(DISTINCT o) as total
MATCH (x:Persona)
WITH p, total, count(x) as all
WHERE total = all - 1
RETURN p.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 64
NIVEL: dificil
ENUNCIADO: Encuentra personas que conectan diferentes ciudades a través de amistad.
SINTAXIS REQUERIDA:
MATCH (a:Persona)-[:AMIGO_DE]->(b:Persona)-[:AMIGO_DE]->(c:Persona),(a)-[:VIVE_EN]->(c1),(c)-[:VIVE_EN]->(c2)
WHERE c1 <> c2
RETURN b.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 65
NIVEL: dificil
ENUNCIADO: Encuentra el nodo más frequent en paths de amistad.
SINTAXIS REQUERIDA:
MATCH p=(a:Persona)-[:AMIGO_DE*]->(b:Persona)
UNWIND nodes(p) as n
RETURN n, count(*) as total
ORDER BY total DESC
LIMIT 1

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 66
NIVEL: medio
ENUNCIADO: Obtén todas las personas junto con la empresa en la que trabajan y la ciudad en la que viven.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:TRABAJA_EN]->(e:Empresa),(p)-[:VIVE_EN]->(c:Ciudad)
RETURN p.nombre, e.nombre, c.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 67
NIVEL: medio
ENUNCIADO: Cuenta cuántas personas trabajan en cada empresa y viven en Madrid.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:TRABAJA_EN]->(e:Empresa),(p)-[:VIVE_EN]->(:Ciudad {nombre:'Madrid'})
RETURN e.nombre, count(p)

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 68
NIVEL: medio
ENUNCIADO: Modifica la consulta para ordenar los resultados por número de empleados descendente.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:TRABAJA_EN]->(e:Empresa)
RETURN e.nombre, count(p) as total
ORDER BY total DESC

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 69
NIVEL: medio
ENUNCIADO: Obtén personas que viven in la misma ciudad que sus compañeros de trabajo.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:TRABAJA_CON]->(o:Persona),(p)-[:VIVE_EN]->(c),(o)-[:VIVE_EN]->(c)
RETURN DISTINCT p.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 70
NIVEL: medio
ENUNCIADO: Corrige la consulta para usar correctamente ORDER BY.
SINTAXIS REQUERIDA:
MATCH (p:Persona)
RETURN p.nombre
ORDER BY p.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 71
NIVEL: medio
ENUNCIADO: Encuentra proyectos gestionados por personas que trabajan en DataSoft.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:TRABAJA_EN]->(:Empresa {nombre:'DataSoft'}),(p)-[:GESTIONA]->(pr:Proyecto)
RETURN pr.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 72
NIVEL: medio
ENUNCIADO: Obtén personas junto con el número de amigos y el número de proyectos en los que participan.
SINTAXIS REQUERIDA:
MATCH (p:Persona)
OPTIONAL MATCH (p)-[:AMIGO_DE]->(a)
WITH p, count(a) as amigos
OPTIONAL MATCH (p)-[:PARTICIPA_EN]->(pr)
RETURN p.nombre, amigos, count(pr)

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 73
NIVEL: medio
ENUNCIADO: Modifica la consulta para mostrar solo personas con al menos un amigo.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:AMIGO_DE]->(a)
WITH p, count(a) as total
WHERE total > 0
RETURN p.nombre, total

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 74
NIVEL: dificil
ENUNCIADO: Encuentra personas cuyos amigos participan en proyectos distintos a los suyos.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:PARTICIPA_EN]->(pr1),(p)-[:AMIGO_DE]->(a:Persona)-[:PARTICIPA_EN]->(pr2)
WHERE pr1 <> pr2
RETURN p.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 75
NIVEL: dificil
ENUNCIADO: Encuentra personas que trabajan con alguien que vive en otra ciudad.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:TRABAJA_CON]->(o:Persona),(p)-[:VIVE_EN]->(c1),(o)-[:VIVE_EN]->(c2)
WHERE c1 <> c2
RETURN p.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 76
NIVEL: dificil
ENUNCIADO: Encuentra personas que comparten al menos una tecnología.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:AMIGO_DE]->(a:Persona)
MATCH (p)-[:USA_TECNOLOGIA]->(t:Tecnologia),(a)-[:USA_TECNOLOGIA]->(t)
RETURN DISTINCT p.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 77
NIVEL: dificil
ENUNCIADO: Corrige la consulta para aplicar correctamente múltiples MATCH.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:TRABAJA_EN]->(e),(p)-[:VIVE_EN]->(c)
RETURN p,e,c

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 78
NIVEL: dificil
ENUNCIADO: Modifica la consulta para devolver solo nombres únicos de personas.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:TRABAJA_CON]->(o:Persona)
RETURN DISTINCT p.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 79
NIVEL: medio
ENUNCIADO: Obtén personas junto con el número total de relaciones que tienen.
SINTAXIS REQUERIDA:
MATCH (p:Persona)--()
RETURN p.nombre, count(*)

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 80
NIVEL: medio
ENUNCIADO: Encuentra personas conectadas a al menos un proyecto a través de cualquier relación.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-->(:Proyecto)
RETURN DISTINCT p.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 81
NIVEL: dificil
ENUNCIADO: Encuentra personas que están a distancia exactamente 2 en la red de amistad.
SINTAXIS REQUERIDA:
MATCH (a:Persona)-[:AMIGO_DE*2..2]->(b:Persona)
RETURN a.nombre, b.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 82
NIVEL: dificil
ENUNCIADO: Modifica la consulta para excluir relaciones directas.
SINTAXIS REQUERIDA:
MATCH (a:Persona)-[:AMIGO_DE*2..2]->(b:Persona)
RETURN a,b

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 83
NIVEL: medio
ENUNCIADO: Encuentra ciudades donde viven personas que trabajan en TechCorp.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:TRABAJA_EN]->(:Empresa {nombre:'TechCorp'}),(p)-[:VIVE_EN]->(c:Ciudad)
RETURN DISTINCT c.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 84
NIVEL: medio
ENUNCIADO: Obtén universidades junto con el número de personas que estudiaron en ellas.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:ESTUDIO_EN]->(u:Universidad)
RETURN u.nombre, count(p)

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 85
NIVEL: medio
ENUNCIADO: Corrige la consulta para usar DISTINCT correctamente.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:VIVE_EN]->(c:Ciudad)
RETURN DISTINCT c.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 86
NIVEL: dificil
ENUNCIADO: Encuentra personas cuyos amigos viven todos en la misma ciudad.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:AMIGO_DE]->(a:Persona),(a)-[:VIVE_EN]->(c:Ciudad)
WITH p, collect(DISTINCT c) as ciudades
WHERE size(ciudades)=1
RETURN p.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 87
NIVEL: dificil
ENUNCIADO: Encuentra personas que trabajan en empresas donde todos los empleados viven en la misma ciudad.
SINTAXIS REQUERIDA:
MATCH (e:Empresa)<-[:TRABAJA_EN]-(p:Persona),(p)-[:VIVE_EN]->(c:Ciudad)
WITH e, collect(DISTINCT c) as ciudades
WHERE size(ciudades)=1
MATCH (e)<-[:TRABAJA_EN]-(p2:Persona)
RETURN p2.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 88
NIVEL: dificil
ENUNCIADO: Encuentra personas que tienen al menos un amigo en cada ciudad.
SINTAXIS REQUERIDA:
MATCH (c:Ciudad)
WITH collect(c) as ciudades
MATCH (p:Persona)-[:AMIGO_DE]->(a:Persona)-[:VIVE_EN]->(c2:Ciudad)
WITH p, collect(DISTINCT c2) as ciudades2, ciudades
WHERE ciudades2 = ciudades
RETURN p.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 89
NIVEL: dificil
ENUNCIADO: Modifica la consulta para limitar a los 3 resultados con más amigos.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:AMIGO_DE]->(a:Persona)
RETURN p.nombre, count(a) as total
ORDER BY total DESC
LIMIT 3

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 90
NIVEL: dificil
ENUNCIADO: Encuentra personas que están conectadas por amistad a alguien que trabaja en todas las empresas.
SINTAXIS REQUERIDA:
MATCH (e:Empresa)
WITH count(e) as total
MATCH (a:Persona)-[:TRABAJA_EN]->(e:Empresa)
WITH a, count(DISTINCT e) as c, total
WHERE c = total
MATCH (p:Persona)-[:AMIGO_DE]->(a)
RETURN p.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 91
NIVEL: dificil
ENUNCIADO: Encuentra personas que tienen más amigos que la media.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:AMIGO_DE]->(a)
WITH p, count(a) as total
WITH collect(total) as totales, p, total
WITH p, total, reduce(s=0, x IN totales | s + x) / size(totales) as media
WHERE total > media
RETURN p.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 92
NIVEL: dificil
ENUNCIADO: Encuentra personas que están conectadas con otras mediante más de un camino distinto.
SINTAXIS REQUERIDA:
MATCH p=(a:Persona)-[:AMIGO_DE*1..3]->(b:Persona)
WITH a,b,count(p) as total
WHERE total > 1
RETURN a.nombre, b.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 93
NIVEL: dificil
ENUNCIADO: Encuentra personas cuyos amigos trabajan en todas las empresas.
SINTAXIS REQUERIDA:
MATCH (e:Empresa)
WITH collect(e) as empresas
MATCH (p:Persona)-[:AMIGO_DE]->(a:Persona)-[:TRABAJA_EN]->(e2:Empresa)
WITH p, collect(DISTINCT e2) as empresas2, empresas
WHERE empresas2 = empresas
RETURN p.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 94
NIVEL: dificil
ENUNCIADO: Encuentra personas que están en todos los caminos entre dos nodos específicos.
SINTAXIS REQUERIDA:
MATCH p=(a:Persona {nombre:'Ana'})-[:AMIGO_DE*]->(b:Persona {nombre:'Carlos'})
UNWIND nodes(p) as n
RETURN n, count(*) as total
ORDER BY total DESC

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 95
NIVEL: dificil
ENUNCIADO: Modifica la consulta para devolver solo los nodos más frecuentes.
SINTAXIS REQUERIDA:
MATCH p=(a)-[:AMIGO_DE*]->(b)
UNWIND nodes(p) as n
RETURN n, count(*) as total
ORDER BY total DESC
LIMIT 1

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 96
NIVEL: medio
ENUNCIADO: Obtén personas junto con todas las ciudades en las que tienen amigos.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:AMIGO_DE]->(a:Persona)-[:VIVE_EN]->(c:Ciudad)
RETURN p.nombre, collect(DISTINCT c.nombre)

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 97
NIVEL: medio
ENUNCIADO: Encuentra empresas donde trabajan personas que usan Python.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:USA_TECNOLOGIA]->(:Tecnologia {nombre:'Python'}),(p)-[:TRABAJA_EN]->(e:Empresa)
RETURN DISTINCT e.nombre

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 98
NIVEL: medio
ENUNCIADO: Corrige la consulta para usar correctamente múltiples relaciones.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:TRABAJA_EN]->(e),(p)-[:VIVE_EN]->(c)
RETURN p,e,c

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 99
NIVEL: medio
ENUNCIADO: Modifica la consulta para devolver solo los 2 proyectos con más participantes.
SINTAXIS REQUERIDA:
MATCH (p:Persona)-[:PARTICIPA_EN]->(pr:Proyecto)
RETURN pr.nombre, count(p) as total
ORDER BY total DESC
LIMIT 2

--------------------------------------------------------------------------------

IDENTIFICADOR: ID 100
NIVEL: dificil
ENUNCIADO: Encuentra personas que maximizan el número de conexiones indirectas en la red de amistad.
SINTAXIS REQUERIDA:
MATCH p=(a:Persona)-[:AMIGO_DE*1..3]->(b:Persona)
RETURN a.nombre, count(DISTINCT b) as total
ORDER BY total DESC
LIMIT 1
