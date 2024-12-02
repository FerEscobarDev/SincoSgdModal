# Sinco SGD Modal

Este paquete amplía la funcionalidad del componente Dialog de MUI, adaptándolo a los diseños de SincoSoft. Proporciona un componente más reutilizable y permite la creación de formularios dinámicos dentro del modal, integrando formik para una gestión eficiente de los formularios.

## Componentes

1. [Componente Modal](#modal)
2. [Componente HeaderModal](#headerModal)
3. [Componente ActionsModal](#actionsModal)
4. [Componente FormModalDinamic](#formModalDinamic)

## Requisitos

- `@mui/icons-material`: >=^5.14.16
- `@mui/material`: >=^5.14.16
- `formik`: >=^2.4.6
- `react`: >=^18.2.0
- `react-dom`: >=^18.2.0
- `yup`: >=^1.4.0

## Instalación
```
npm i sinco-sgd-modal
```

## Ejemplos de uso del componente Modal

### Ejemplo 1: Modal de Confirmación

```tsx
import { Box, Button, DialogContent, Typography } from '@mui/material';
import { useState } from 'react';
import { Dashboard } from '@mui/icons-material';
import { ActionsModal, HeaderModal, Modal } from './components';
import { grey } from '@mui/material/colors';

function App() {
    const [ abrirModal, setAbrirModal ] = useState(false);

    const handleCierreModal = () => setAbrirModal(!abrirModal);

    return (
        <>
            <Button variant='contained' color='primary' size='small' startIcon={<Dashboard/>} onClick={handleCierreModal}>Abrir Modal</Button>

            <Modal
                open={abrirModal} 
                headerProps={{
                    titulo:'Está Seguro?',
                    headerAlerta:true,
                    tipoAlerta:'danger'
                }}
                actionsProps={{
                    nombreBoton:'Aceptar',
                    colorButton:'error',
                    sxActionsContainer:{backgroundColor:grey[50]}
                }}
                maxWidth='xs'
            >
                <HeaderModal/>
                <DialogContent>
                    <Box sx={{display:'flex', flexDirection:'column', justifyContent:'center', alignItems:'normal',gap:2}}>                        
                        <Typography variant='body2' color="text.primary">Este es el mensaje para confirmar</Typography>
                    </Box>
                </DialogContent>
                <ActionsModal/>
            </Modal>
        </>
    );
}

export default App;
```
### Ejemplo 2: Modal con Formulario Dinámico

```tsx
import { Box, Button, DialogContent, Typography } from '@mui/material';
import { useState } from 'react';
import { Dashboard } from '@mui/icons-material';
import { ActionsModal, FormModalDinamic, HeaderModal, Modal } from './components';
import { FormikValues } from 'formik';

function App() {
    const [ abrirModal2, setAbrirModal2 ] = useState(false);

    const handleCierreModal2 = () => setAbrirModal2(!abrirModal2);

    const Guardar = (arg? : FormikValues) => {
        handleCierreModal2();
        console.log("Valores",arg)
    };

    const form = {
        initialValues: {nombre:'', apellido:'', email:'', terms:false},
        formFields: [
            {name:'nombre', label:'Nombre', tipo:'textField', variant: "outlined", placeholder:'Ingrese su nombre', 
                validations:[
                    {type:'required'},
                    {type:'min', value:3},
                    {type:'max', value:20}
                ] },
            {name:'apellido', label:'Apellido', tipo:'textField', variant:'outlined', placeholder:'Ingrese su apellido', 
                validations:[
                    {type:'required'},
                    {type:'min', value:3},
                    {type:'max', value:20}
                ]
            },
            {name:'email', label:'Email', tipo:'textField', variant:'outlined', placeholder:'Ingrese su email', 
                validations:[
                    {type:'required'},
                    {type:'email'}
                ]
            },
            {name:'terms', label:'Acepta los términos y condiciones?', tipo:'checkbox', 
                validations:[
                    {type:'oneOf', value:['true']}
                ]
            }
        ]
    };

    return (
        <>
            <Button variant='contained' color='primary' size='small' startIcon={<Dashboard/>} onClick={handleCierreModal2}>Abrir Modal</Button>

            <Modal 
                open={abrirModal2} 
                headerProps={{
                    titulo:'Formulario',
                    imagen:'https://www.w3schools.com/howto/img_avatar.png',
                }}
                actionsProps={{
                    nombreBoton:'Aceptar',
                    colorButton:'primary',
                    handleAccion:Guardar
                }}
                maxWidth='xs'
            >
                <HeaderModal/>
                <FormModalDinamic initialValues={form.initialValues} formFields={form.formFields}/>
            </Modal>
        </>
    );
}

export default App;
```
### Ejemplo 3: Modal con Contenido personalizado

```tsx
import { Box, Button, DialogContent, Typography } from '@mui/material';
import { useState } from 'react';
import { Dashboard } from '@mui/icons-material';
import { ActionsModal, Modal } from './components';

function App() {
    const [ abrirModal3, setAbrirModal3 ] = useState(false);

    const handleCierreModal3 = () => setAbrirModal3(!abrirModal3);

    return (
        <>
            <Button variant='contained' color='primary' size='small' startIcon={<Dashboard/>} onClick={handleCierreModal3}>Abrir Modal</Button>

            <Modal 
                open={abrirModal3}
                actionsProps={{
                    nombreBoton:'Aceptar',
                    colorButton:'primary',
                    handleAccion:handleCierreModal3
                }}
                maxWidth='xs'
            >
                <DialogContent>
                    <Box sx={{display:'flex', flexDirection:'column', justifyContent:'center', alignItems:'normal', gap:2}}>
                        <Typography variant='body2' color="text.primary">Lorem ipsum dolor sit amet consectetur adipisicing elit. 
                            Totam et uibusdam iste dignissimos quam doloribus voluptatum dolore delectus, nihil excepturi labore 
                            distinctio consequatur, animi eaque est saepe quas repellendus dolor.
                        </Typography>
                    </Box>
                </DialogContent>
                <ActionsModal/>
            </Modal>
        </>
    );
}

export default App;
```