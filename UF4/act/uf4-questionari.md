# Qüestionari d'autoavaluació de la UF4

<quiz name="">
    <question>
        <p>El CUPS serveix... </p>
        <answer>Per compartir carpetes</answer>
        <answer correct>Per compartir impressores</answer>
        <answer>Per compartir tasques</answer>
        <answer>Cap resposta es vàlida</answer>
    </question>
    
    <question>
        <p>En el fitxer de configuració del NFS hem d'indicar en aquest ordre...</p>
        <answer>Amb qui, com i què compartim.</answer>
        <answer>Què, com i amb qui ho compartim.</answer>
        <answer correct>Què, com i amb qui ho compartim.</answer>
        <answer>Amb qui, què i com ho compartim.</answer>
    </question>

    <question>
        <p>En Sistemes Linux, en quin fitxer es configura el muntatge automàtic?</p>
        <answer>/etc/shares</answer>
        <answer>/etc/mount</answer>
        <answer>/etc/exports</answer>
        <answer correct>/etc/fstab</answer>
    </question>
    
    <question>
        <p>En Windows, per connetar-se a una unitat de xarxa el recurs compartit Dades del servidor 192.168.1.10, cal executar:</p>
        <answer correct>net use z:  \\192.168.1.10\Dades</answer>
        <answer>net share \\192.168.1.10\Dades </answer>
        <answer>mount \\192.168.1.10\Dades</answer>
        <answer>mount z:  \\192.168.1.10\Dades</answer>
    </question>
    
    <question>
        <p>En Windows, com podem compartir de manera oculta una carpeta?</p>
        <answer>Posant $ a l'inici del seu nom.  </answer>
        <answer correct>Posant $ al final del seu nom. </answer>
        <answer>Posant % a l'inici del seu nom. </answer>
        <answer>Posant % al final del seu nom. </answer>
    </question>  
    
    <question>
        <p>On ha d'estar el recurs compartit NFS? Al sistema operatiu Linux...</p>
        <answer correct>servidor</answer>
        <answer>client</answer>
        <answer>a tots dos (al client i servidor)</answer>
        <answer>al que vulguem (al client o al servidor)</answer>
    </question>
    
    <question>
        <p>On trobem el fitxer de configuració del NFS?</p>
        <answer>/etc/fstab</answer>
        <answer correct>/etc/exports</answer>
        <answer>/etc/nfs/exports</answer>
        <answer>/etc/nfs/exportt</answer>
    </question>

    <question>
        <p>Els grups de l'Active Directory NO poden contenir: </p>
        <answer>Altres grups. </answer>
        <answer correct>Unitat organitzativa.</answer>
        <answer>Usuaris. </answer>
        <answer>Equips. </answer>
    </question>
    
    <question>
        <p>Si un client NFS vol muntar el directori “/srv/nfs” exportat des del servidor NFS que té IP 192.168.31.2, cal executar:</p>
        <answer>mount –t nfs  /srv/nfs   192.168.31.2:/srv/nfs</answer>
        <answer correct>mount –t nfs 192.168.31.2:/srv/nfs  /srv/nfs </answer>
        <answer>mount –p nfs 192.168.31.2:/srv/nfs</answer>
        <answer>mount –p 192.168.31.2:/srv/nfs   /svr/nfs</answer>
    </question>
</quiz>