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
  <li>Correo del emplieado</li>
</ul>
<br/>
<pre>
  <code>
    Dim msg As String = firma.cancelaUsuario("correEmpleado@correo.com")
  </code>
</pre>

<p>El resultado de la llamada regresará un mensaje el cual indica si el usuario fue o no cancelado con exito</p>

### WebConfig ###

<p> Es necesario agregar la siguiente sección al archivo <code>Web.config</code>
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
