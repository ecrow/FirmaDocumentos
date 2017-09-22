# FirmaDocumento

FirmaDocumento es una librería desarrollada en Visual Basic .Net la cual implementa Servicios Web de Doc2Sign y la cual expone 2 métodos y la confirguación de un Widget para firma de documentos. 


# Instalación
<ol>
  <li>Descarga la mas reciente versión</li>
  <li>Importa FirmaDocumento.dll a tu proyecto</li>
  <li>Configura el archivo Web.config agregando los endpoints correspondientes.</li>
<ol>
  
# Uso

Crea una instancia de la clase 
<pre>
  <code>
    Dim Firma as Firma = new Firma()
  </code>
</pre>

# Configuración del Widget

Inserta un elemento IFrame con las siguientes características
<pre>
  <code>
    <iframe id="iFrameWidget" runat="server" width="100%" height="550px"></iframe>
  </code>
</pre>
El valor del atributo id del elemento IFrame puede ser personalizado
