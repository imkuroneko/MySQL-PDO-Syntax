# MySQL PDO

#### Conectar a la base de datos:



    define('db_server' ,  "");    # Servidor
    define('db_name'   ,  "");    # Nombre de la base de datos
    define('db_user'   ,  "");    # Usuario
    define('db_pass'   ,  "");    # Contraseña


    try {

      $mysql  =   new PDO('mysql:host='. db_server .';dbname='. db_name , db_user , db_pass);
      $mysql  ->  setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);

    } catch(PDOException $e) {
      echo $e->getMessage();
    }

####  Consulta : Todo

        $query      =   'SELECT * FROM {table}';

        $consult    =   $mysql -> query($query);
        $consult    ->  setFetchMode(PDO::FETCH_ASSOC);

####  Consulta : Condicionado (x string)

      $query      =   'SELECT * FROM {table} WHERE {column_name} = :{var_name}';

      $consult    =   $mysql -> prepare($query);
      $consult    ->  execute([':{var_name}' => '{value}']);
      $consult    ->  setFetchMode(PDO::FETCH_ASSOC);

####  Consulta : Imprimir Resultados

        <table>
        <?php while ($print = $consult->fetch()): ?>
            <tr>
                <td> <?php echo $print['{column_name1}']; ?> </td>
                <td> <?php echo $print['{column_name2}']; ?> </td>
                <td> <?php echo $print['{column_name3}']; ?> </td>
                ...
            </tr>
        <?php endwhile; ?>
        </table>

####  Actualizar Datos

      $query      =   'UPDATE {table} SET {column_name1} = :{var_name1}, {column_name2} = :{var_name2}, ... WHERE {column_id} = :id';
      
      $update     =   $mysql -> prepare($query);
      $update     ->  execute([':id' => {value}, ':{column_name1}' => '{var_name1}', {column_name2} = :{var_name2}, ...]);

####  Eliminar Datos

      $query      =   'DELETE FROM {table} WHERE {column_name} = :{var_name}';
      
      $delete     =   $mysql -> prepare($query);
      $delete     ->  execute([':id' => {value}]);

####  Insertar Datos

      $query      =   'INSERT INTO {table} ({column_name1}, {column_name2}, ...) VALUES (:{var_name1}, :{var_name2}, ...) ';
      
      $insert     =   $mysql -> prepare($query);
      $insert     ->  execute([':{var_name1}' => '{value}', ':{var_name2}' => '{value}', ...]);
