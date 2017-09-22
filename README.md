# FirmaDocumento

FirmaDocumento es una librería desarrollada en Visual Basic .Net la cual implementa Servicios Web de Doc2Sign y la cual expone 2 métodos y la confirguación de un Widget para firma de documentos. 


# Instalación
<ol>
  <li>Descarga la mas reciente versión</li>
  <li>Importa <code>FirmaDocumento.dll</code> a tu proyecto</li>
  <li>Configura el archivo Web.config agregando los endpoints correspondientes.</li>
<ol>
  
# Uso

Crea una instancia de la clase <code>Firma</code>
<pre>
  <code>
    Dim Firma as Firma = new Firma()
  </code>
</pre>

# Configuración del Widget

Inserta un elemento <code>IFrame</code> con las siguientes características
<pre>
  <code>
    <iframe id="iFrameWidget" runat="server" width="100%" height="550px"></iframe>
  </code>
</pre>
El valor del atributo id del elemento IFrame puede ser personalizado
### Métodos ###
###### getIframeContent
<p>Para inicializar el atributo <code>src</code> del Widget, es necesario implementar el método <code>getIframeContent</code> de la clase <code>Firma</code> utilizando como parámetro el correo del empleado</p>
<pre>
  <code>
    iFrameWidget.Attributes("src") = firma.getIframeContent("correoEmpleado@correo.com")
  </code>
</pre>

<p>Esto desplegará en el IFrame un componente como el siguiente</p>
<img src="https://github.com/ecrow/FirmaDocumentos/blob/master/images/Widget1.png" alt="Widget 1"/>


<p>El empleado introduce la contraseña con la cual fue registrado en Doc2sign y la cual le fue enviada a su correo electrónico</p>


