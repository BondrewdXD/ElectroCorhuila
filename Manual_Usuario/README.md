# 📘 Manual de Usuario - Sistema de Gestión de Usuarios y Tarifas

## Parte Frontend - Interfaz de Usuario

---

### 🎯 Propósito del Sistema

El sistema permite a los usuarios finales gestionar su información personal y consultar las tarifas asignadas según su estrato socioeconómico. Desarrollado con **Ionic y React** para ofrecer una experiencia moderna y responsiva.

---

### 🧭 Guía de Navegación

#### Inicio

Al ingresar al sistema, se presenta una interfaz intuitiva donde el usuario puede:

- Visualizar un formulario para registrar sus datos  
- Consultar información relacionada con la tarifa asignada



![Img_Inicio](inicio.png)



---

### 🖥️ Pantallas del Sistema

#### 1. Formulario de Usuario

📂 **Ubicación en el proyecto:** `src/component/FormularioUsuario.tsx`

```
import {
  IonButton,
  IonContent,
  IonInput,
  IonItem,
  IonLabel,
  IonList,
  IonPage,
  IonTitle,
  IonToolbar,
  IonHeader,
  IonCard,
  IonCardContent,
} from '@ionic/react';
import { useState } from 'react';
import { useHistory } from 'react-router-dom';
import './FormularioUsuario.css';

const FormularioUsuario: React.FC = () => {
  const [nombre, setNombre] = useState('');
  const [direccion, setDireccion] = useState('');
  const [estrato, setEstrato] = useState<number | undefined>(undefined);
  const [mensaje, setMensaje] = useState('');
  const history = useHistory();

  const handleSubmit = async () => {
    const usuario = { nombre, direccion, estrato };

    try {
      const response = await fetch('http://localhost:8080/usuarios', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(usuario),
      });

      if (response.ok) {
        const data = await response.json(); // Obtener la respuesta del backend
        history.push('/estrato', {
          nombre: data.nombre,
          estrato: data.estrato,
        });
      } else {
        setMensaje('❌ Error al crear el usuario');
      }
    } catch (error) {
      setMensaje('❌ Error de conexión con el servidor');
    }
  };

  return (
    <IonPage>
      <IonHeader>
        <IonToolbar className="header-card">
          <IonTitle>Registrar Usuario</IonTitle>
        </IonToolbar>
      </IonHeader>

      <IonContent className="ion-padding content-bg">
        <IonCard className="form-card">
          <IonCardContent>
            <IonList>
              <IonItem className="input-item">
                <IonLabel position="floating">Nombre</IonLabel>
                <IonInput
                  value={nombre}
                  onIonChange={(e) => setNombre(e.detail.value!)}
                />
              </IonItem>

              <IonItem className="input-item">
                <IonLabel position="floating">Dirección</IonLabel>
                <IonInput
                  value={direccion}
                  onIonChange={(e) => setDireccion(e.detail.value!)}
                />
              </IonItem>

              <IonItem className="input-item">
                <IonLabel position="floating">Estrato</IonLabel>
                <IonInput
                  type="number"
                  min={1}
                  max={4}
                  value={estrato}
                  onIonChange={(e) => {
                    const value = parseInt(e.detail.value!);
                    if (!isNaN(value) && value >= 1 && value <= 4) {
                      setEstrato(value);
                    } else {
                      setEstrato(undefined);
                    }
                  }}
                />
              </IonItem>
            </IonList>

            <IonButton expand="block" color="primary" onClick={handleSubmit}>
              Registrar
            </IonButton>

            {mensaje && <p className="mensaje">{mensaje}</p>}
          </IonCardContent>
        </IonCard>
      </IonContent>
    </IonPage>
  );
};

export default FormularioUsuario;
```

**Campos disponibles:**

- Nombre completo  
- Dirección
- Estrato socioeconómico (selección)

**Funciones disponibles:**

- Ingresar la información del usuario  
- Enviar datos al servidor mediante `UsuarioService`

```
const API_URL = "http://localhost:8080/usuarios"; // Conexión del Backend y Frontend

export interface CrearUsuarioRequest {
  nombre: string;
  direccion: string;
  estrato: number;
}

export async function crearUsuario(data: CrearUsuarioRequest) {
  const response = await fetch(API_URL, {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(data),
  });

  if (!response.ok) {
    throw new Error("Error al crear el usuario");
  }

  return await response.json();
}
```
### Explicación paso a paso:

#### 1.  Definición de la URL de la API
Con el uso de la constante API_URL define la dirección donde el backend está esperando recibir solicitudes para gestionar la data.

#### 2.  Interfaz CrearUsuarioRequest
La interfaz CrearUsuarioRequest determina la estructura de los datos que se enviarán desde el frontend al backend. En este caso, el objeto solo puede contener tres propiedades:
> nombre.
> dirección.
> estrato.
 
---

### ⚙️ Funcionalidades Principales

#### ✅ Registro y edición de usuario

El formulario permite al usuario ingresar su información o actualizarla. Al enviar, se realiza una llamada al backend a través del archivo `UsuarioService.ts`.

#### 🔄 Comunicación con el backend

La lógica para la comunicación HTTP está centralizada en `UsuarioService.ts`, utilizando `fetch` para enviar y recibir datos del servidor.
