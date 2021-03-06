# Primeros pasos

## Instalar iqoptionapi

descarga el código fuente y ejecuta lo siguiente:

```
python setup.py install
```

## Un ejemplo simple

```python
import time
from iqoptionapi.stable_api import IQ_Option
I_want_money=IQ_Option("email","password")
I_want_money.connect()#connect to iqoption
goal="EURUSD"
print("get candles")
print(I_want_money.get_candles(goal,60,111,time.time()))
```

## Importar la librería

```python
from iqoptionapi.stable_api import IQ_Option
```

## Login

I_want_money.connect() will return (check,reason)

Si la conexión es exitosa, devuelve -> True,None

Si hay algún fallo en la conexión, devuelve -> False,reason

```python
from iqoptionapi.stable_api import IQ_Option
import logging

logging.basicConfig(level=logging.DEBUG,format='%(asctime)s %(message)s')
I_want_money=IQ_Option("email","password")
check, reason=I_want_money.connect()#connect to iqoption
print(check, reason)
```

## Activar el modo Debug

```python
import logging
logging.basicConfig(level=logging.DEBUG,format='%(asctime)s %(message)s')
```

## Conectarse y comprobar la conexión

A veces la conexión se cierra, así que debemos de comprobar la conexión y
volvenos a conectar.

Prueba a desconectar tu conexión y volverla a conectar para probar el siguiente
ejemplo.

```python
from iqoptionapi.stable_api import IQ_Option
error_password="""{"code":"invalid_credentials","message":"You entered the wrong credentials. Please check that the login/password is correct."}"""
iqoption = IQ_Option("email", "password")
check,reason=iqoption.connect()
if check:
    print("Activa tu robot")
    #Si ves esto puedess cerrar la conexión para probarlo
    while True:
        if iqoption.check_connect()==False:#Detecta si el websocket ha sido cerrado
            print("Probando a reconectar")
            check,reason=iqoption.connect()
            if check:
                print("Reconectado con éxito")
            else:
                if reason==error_password:
                    print("Contraseña incorrecta")
                else:
                    print("No hay conexión")

else:

    if reason=="[Errno -2] Nombre or servicio no conocido":
        print("No hay conexión")
    elif reason==error_password:
        print("Error en la Contraseña")
```

## set_session

Default User-Agent is "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3359.139 Safari/537.36"

```python
from iqoptionapi.stable_api import IQ_Option
import logging
logging.basicConfig(level=logging.DEBUG,format='%(asctime)s %(message)s')

I_want_money=IQ_Option("email","password")

#Por defecto es "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3359.139 Safari/537.36"

header={"User-Agent":r"Mozilla/5.0 (X11; Linux x86_64; rv:70.0) Gecko/20100101 Firefox/70.0"}
cookie={"I_want_money":"GOOD"}

I_want_money.set_session(header,cookie)

I_want_money.connect()#Conectar a IqOption
```

## Comprobar versión

```python
from iqoptionapi.stable_api import IQ_Option
print(IQ_Option.__version__)
```

## Comprobar conexión

return True/False

```
print(I_want_money.check_connect())
```

## Reconnect

```python
I_want_money.connect()
```

## time

get_server_timestamp
El tiempo se sincronica con iqoption

```python
I_want_money.get_server_timestamp()
```
