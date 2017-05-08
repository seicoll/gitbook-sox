# Qüestionari d'autoavaluació de la UF4

<quiz name="">
    <question>
        <p>El Samba permet controlar quins usuaris podran accedir als recursos compartits. Com administra els usuaris el Samba?</p>
        <answer>No requereix treballar amb usuaris.</answer>
        <answer>Utilitza qualsevol usuari del Windows.</answer>
        <answer>Utilitza qualsevol usuari del GNU/Linux.</answer>
        <answer correct>Té la seva pròpia base de dades d'usuaris.</answer>
    </question>
    
    <question>
        <p>El protocol utilitzat pels sistemes operatius Windows per compartir carpetes i impressores és...</p>
        <answer correct>SMB o actualment CIFS</answer>
        <answer>SAMBA o actualment CIFS</answer>
        <answer>NFS</answer>
        <answer>Totes són correctes.</answer>
    </question>

    <question>
        <p>Per tal que els usuaris tinguin els mateix escriptori, accés als seus documents i configuracions des de qualsevol equip del domini on es connectin, cal configurar...</p>
        <answer>el permil remot.</answer>
        <answer>el perfil de xarxa.</answer>
        <answer correct>el perfil mòbil.</answer>
        <answer>el perfil local.</answer>
    </question>
    
    <question>
        <p>En Windows, per connetar-se a una unitat de xarxa el recurs compartit Dades del servidor 192.168.1.10, cal executar:</p>
        <answer correct>net use z:  \\192.168.1.10\Dades</answer>
        <answer>net share \\192.168.1.10\Dades </answer>
        <answer>mount \\192.168.1.10\Dades</answer>
        <answer>mount z:  \\192.168.1.10\Dades</answer>
    </question>
    
    <question>
        <p>Per unir un client Linux a un domini Windows, quin paquet hem utilitzat que s'encarrega de la major part de la configuració del sistema?</p>
        <answer>smbclient</answer>
        <answer>domain-join </answer>
        <answer correct>pbis-open</answer>
        <answer>samba</answer>
    </question>  
    
    <question>
        <p>Quan els permisos GNU/Linux es contradiuen amb els permisos Samba, el permís efectiu és:</p>
        <answer>El permís Samba</answer>
        <answer>El permís GNU/Linux</answer>
        <answer correct>El més restrictiu</answer>
        <answer>El més permissiu</answer>
    </question>
</quiz>