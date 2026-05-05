<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Pacientes</title>
    <style>
        table {
            border-collapse: collapse;
            width: 60%;
            margin: 20px auto;
        }
        th, td {
            border: 1px solid #000;
            padding: 8px;
            text-align: center;
        }
        th {
            background-color: #ddd;
        }
        h1 {
            text-align: center;
        }
    </style>
</head>

<body>
    <h1>Pacientes</h1>

    <table>
        <tr>
            <th>Nombre</th>
            <th>Edad</th>
        </tr>

        <?php 
        require 'vendor/autoload.php';

        try {
            // Conexión a MongoDB
            $client = new MongoDB\Client("mongodb://localhost:27987");

            // Base de datos y colección
            $collection = $client->Clinica->pacientes;

            // Consulta
            $result = $collection->find();

            // Mostrar en tabla
            foreach ($result as $pac) {
                echo "<tr>";
                echo "<td>" . $pac['nombre'] . "</td>";
                echo "<td>" . $pac['edad'] . "</td>";
                echo "</tr>";
                
            }

        } catch (Exception $e) {
            echo "<tr><td colspan='2'>Error: " . $e->getMessage() . "</td></tr>";
        }
        ?>
    </table>

</body>
</html>
