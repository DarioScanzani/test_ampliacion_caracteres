# test_ampliacion_caracteres

# Ampliar el Límite de Caracteres

## Pasos a Seguir

### 1. Modificar la Base de Datos

Primero, actualizaria el esquema de la base datos para permitir nombre y apellidos más largos.

1. **Ejecutar la consulta SQL**:
   ```sql
   ALTER TABLE customer_firstname MODIFY firstname VARCHAR(512);
   ALTER TABLE customer_lastname MODIFY lastname VARCHAR(512);
   ```

### 2. Modificar el modelo de datos

2. **Modificar el modelo de datos**.**
Después de actualizar el esquema, nos aseguramos que el modelo de datos reconozca el nuevo límite.

```php
public static $definition = array(
    'fields' => array(
        'firstname' => array('type' => self::TYPE_STRING, 'validate' => 'isName', 'size' => 512),
        'lastname' => array('type' => self::TYPE_STRING, 'validate' => 'isName', 'size' => 512),
        ...
    ),
);
```

### 3. Modificar la validacion del formulario

3. **Anadir la validación del formulario**.

Nos aseguramos de que la interfaz de usuario también permite nombres largos.

```php
$this->validateFields();
if (Tools::strlen($firstname) > 512 || Tools::strlen($lastname) > 512) {
    $this->errors[] = $this->trans('The name or surname is too long.', array(), 'Admin.Notifications.Error');
}
```