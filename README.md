# FirmaDocumento

FirmaDocumento es una librería desarrollada en Visual Basic .Net la cual implementa Servicios Web de Doc2Sign y la cual expone 2 métodos y la confirguación de un Widget para firma de documentos. 


# Instalación
<ol>
  <li>Descarga la mas reciente versión</li>
  <li>Importa <code>FirmaDocumento.dll</code> a tu proyecto</li>
  <li>Configura el archivo Web.config agregando los endpoints correspondientes. (Vease el final de este documento) </li>
</ol>

# Uso
<p>Utiliza el namespace <code>FirmaDocumento</code></p>
<pre>
  <code>
    Imports FirmaDocumento
  </code>
</pre>

Crea una instancia de la clase <code>Firma</code>
<pre>
  <code>
    Dim Firma as Firma = new Firma()
  </code>
</pre>

<p>La clase <code>Firma</code> implementa 3 métodos y 3 propiedades</p>
<h3> Métodos </h3>
<ul>
  <li>getIframeContent</li>
  <li>agregaUsuario</li>
  <li>cancelaUsuario</li>
  <li>getRecibosPendientes</li>
</ul>
<h3> Propiedades </h3>
<ul>
  <li>urlWidget</li>
  <li>usuarioEmpresa</li>
  <li>llaveEmpresa</li>
</ul>

# Configuración del Widget

Inserta un elemento <code>IFrame</code> con las siguientes características

<pre>
  <code>
    <iframe id="iFrameWidget" runat="server" width="100%" height="550px"></iframe>
  </code>
</pre>

El valor del atributo id del elemento IFrame puede ser personalizado
### Métodos ###
##### -getIframeContent
<p>Para inicializar el atributo <code>src</code> del Widget, es necesario implementar el método <code>getIframeContent</code> de la clase <code>Firma</code> utilizando como parámetro el correo del empleado</p>
<pre>
  <code>
    iFrameWidget.Attributes("src") = firma.getIframeContent("correoEmpleado@correo.com")
  </code>
</pre>

<p>Esto desplegará en el IFrame un componente como el siguiente</p>
<img src="https://github.com/ecrow/FirmaDocumentos/blob/master/images/Widget1.png" alt="Widget 1"/>
<hr/>
<p>El empleado introduce la contraseña con la cual fue registrado en Doc2sign y la cual le fue enviada a su correo electrónico</p>

<p>Si la contraseña es valida el widget desplegara el listado de recibos pendientes por firma correspondientes al empleado</p>
<img src="https://github.com/ecrow/FirmaDocumentos/blob/master/images/Widget2.png" alt="Widget 1"/>

##### -agregaUsuario
<p>El método <code>agregaUsuario</code> permite registrar en Doc2sign a un nuevo usuario, los parámetros de este método son los siguientes</p>
<ul>
  <li>Nombre del empleado</li>
  <li>Apellido paterno del empleado</li>
  <li>Apellido materno del empleado</li>
  <li>Correo Electrónico del empleado</li>
  <li>RFC del empleado</li>
</ul>
<br/>
<em>Todos los parámetros son de carácter obligatorio</em>

<pre>
  <code>
    Dim msg As String = firma.agregaUsuario("nombre empleado", "apaterno empleado", "amaterno empleado", "correEmpleado@correo.com", "RFC empleado")
  </code>
</pre>

<p>El resultado de la llamada regresará un mensaje el cual indica si el usuario fue o no registrado con exito</p>

##### -cancelaUsuario

<p>El método <code>cancelaUsuario</code> permite cancelar en Doc2sign a un nuevo usuario, este método utiliza el siguiente parámetro</p>
<ul>
  <li>Correo del empleado</li>
</ul>
<br/>
<pre>
  <code>
    Dim msg As String = firma.cancelaUsuario("correoEmpleado@correo.com")
  </code>
</pre>

<p>El resultado de la llamada regresará un mensaje el cual indica si el usuario fue o no cancelado con exito</p>

##### -getRecibosPendientes

<p>El método <code>getRecibosPendientes</code> permite obtener el número de recibos que el empleado tiene en estatus de "Pendientes", este método utiliza el siguiente parámetro</p>
<ul>
  <li>Correo del empleado</li>
</ul>
<br/>
<pre>
  <code>
    Dim recibosPendientes As Integer = firma.getRecibosPendientes("correoEmpleado@correo.com")
  </code>
</pre>

<p>El resultado de la llamada regresará un valor entero indicando el número de recibos que el empleado tiene pendientes por firma, en caso de error este método regresara un valor negativo -1 </p>

<h3>Propiedades</h3>

<h5>-urlWidget</h5>
<p>Esta propiedad permite obtener y establecer la URL de acceso al widget</p>
<p>La clase <code>Firma</code> está configurada para acceder a una URL de prueba por default
  
<pre>
  <code>
  Cambia la URL del Widget
  firma.urlWidget = "URL del Widget"
  </code>
  <code>
  Obtiene la URL del Widget
  Dim url as String = firma.urlWidget 
  </code>
</pre>

<h5>-usuarioEmpresa</h5>
<p>Esta propiedad permite obtener y establecer la clave de acceso al servicio Web</p>
<p>La clase <code>Firma</code> está configurada para acceder con una clave de prueba por default
  
<pre>
  <code>
  Cambia la clave de acceso 
  firma.usuarioEmpresa = "000000"
  </code>
  <code>
  Obtiene la clave de acceso
  Dim usuario as String = firma.usuarioEmpresa 
  </code>
</pre>

<h5>-llaveEmpresa</h5>
<p>Esta propiedad permite obtener y establecer la llave de acceso al servicio Web</p>
<p>La clase <code>Firma</code> está configurada para acceder con una llave de prueba por default
  
<pre>
  <code>
  Cambia la llave de acceso 
  firma.llaveEmpresa = "000000"
  </code>
  <code>
  Obtiene la llave de acceso 
  Dim empresa as String = firma.llaveEmpresa 
  </code>
</pre>

### WebConfig ###

<p> Es necesario agregar la siguiente sección al archivo <code>Web.config</code> como parte de la configuración de acceso al Servicio Web</p>
<pre>
  <code>
  &ltsystem.serviceModel&gt
    &ltbindings&gt
      &ltbasicHttpBinding&gt
        &ltbinding name="BasicHttpBinding_IConnect" /&gt
        &ltbinding name="BasicHttpsBinding_IConnect"&gt
          &ltsecurity mode="Transport" /&gt
        &lt/binding&gt
      &lt/basicHttpBinding&gt
    &lt/bindings&gt
    &ltclient&gt
      &ltendpoint address="https://test.doc2sign.com/wssimpleconnect/Connect.svc"
       binding="basicHttpBinding" bindingConfiguration="BasicHttpsBinding_IConnect"
       contract="IConnect" name="BasicHttpsBinding_IConnect" /&gt
    &lt/client&gt
  &lt/system.serviceModel&gt
  </code>
</pre>
