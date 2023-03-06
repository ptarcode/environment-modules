# Environment Modules

O pacote Modules é uma ferramenta que simplifica a inicialização do shell e permite que os usuários modifiquem facilmente seu ambiente durante uma sessão usando modulefiles.

Cada arquivo de módulo contém as informações necessárias para configurar o shell para um aplicativo. Depois que o pacote Modules é inicializado, o ambiente pode ser modificado por módulo usando o comando module que interpreta modulefiles. Normalmente, os arquivos de módulo instruem o comando do módulo a alterar ou definir as variáveis ​​de ambiente do shell, como PATH, MANPATH, etc. Os arquivos de módulo podem ser compartilhados por muitos usuários em um sistema e os usuários podem ter sua própria coleção para complementar ou substituir os arquivos de módulo compartilhados.

Os módulos podem ser carregados e descarregados dinâmica e atomicamente, de forma limpa. Todos os shells populares são suportados, incluindo bash, ksh, zsh, sh, csh, tcsh, fish, cmd, bem como algumas linguagens de script como tcl, perl, python, ruby, cmake e r.

Os módulos são úteis no gerenciamento de diferentes versões de aplicativos. Os módulos também podem ser agrupados em metamódulos que carregarão um conjunto completo de aplicativos diferentes.


### Instalação

A instalação pode ser feito usando o gerenciador de pacotes da sua distribuição Linux ou baixando o pacote de instalação.

```
curl -LJO https://github.com/cea-hpc/modules/releases/download/v5.2.0/modules-5.2.0.tar.gz
$ tar xfz modules-5.2.0.tar.gz
```

O jeito simples de afetuar o build e a instalação do Modules:

```
$ ./configure
$ make
$ make install

```


### Exemplos de inicialização

C Shell initialization (and derivatives):
```
source /usr/share/Modules/init/csh
module load modulefile modulefile ...
```
Bourne Shell (sh) (and derivatives):
```
. /usr/share/Modules/init/sh
module load modulefile modulefile ...
```
Perl:
```
require "/usr/share/Modules/init/perl.pm";
&module("load modulefile modulefile ...");
```
Python:
```
import os
exec(open('/usr/share/Modules/init/python.py').read())
module('load modulefile modulefile ...')
```
Bourne Shell (sh) (and derivatives) with autoinit sub-command:
```
eval "`/usr/share/Modules/libexec/modulecmd.tcl sh autoinit`"
```

### Comandos


#### Lista os módulos disponíveis

The command to list available modules is ***module avail***
```
[root@host ~]# module avail

------------------------------------------------------------------------------------- /usr/share/modules --------------------------------------------------------------------------------------
dot  module-git  module-info  modules  null  nvhpc/23.1  use.own <L>  

------------------------------------------------------------------------------------ /root/privatemodules -------------------------------------------------------------------------------------
null  

Key:
<module-tag>  <L>=loaded

```

#### Lista os módulos carregados

Você pode listar os módulos carregados com o comando ***module list***.
```
[root@host ~]# module list
Currently Loaded Modulefiles:
1) mpi/openmpi-interconnects-gnu
```

#### Load a Modulefile

Para carregar o Modulefile você precisa usar o comando ***moduleload***.
```
[root@host ~]# module load mpi/openmpi-interconnects-gnu
```


#### Unload a Modulefile

Para descarregar o modulefile você precisa executar o comando ***module unload***.
```
[root@host ~]# module list
Currently Loaded Modulefiles:
1) mpi/openmpi-interconnects-gnu
```

```
[root@host ~]# module unload mpi/openmpi-interconnects-gnu
[root@host ~]# module list
No Modulefiles Currently Loaded.

```
#### Mostrar informações sobre o Modulefile

Para mostrar informações sobre os modulefiles você precisa executar o comando ***module whatis***.

```
[root@host ~]# module whatis
------------------------------------------------------------------------------------- /usr/share/modules --------------------------------------------------------------------------------------
                 dot: adds `.' to your PATH environment variable
          module-git: get last version of the module sources from GitHub
         module-info: returns all various module-info values
             modules: loads the modules environment
                null: does absolutely nothing
             use.own: adds your own modulefiles directory to MODULEPATH
```

### Exemplo de Modulefile

```
#%Module1.0#####################################################################
##
##  rh-python36 modulefile
##
proc ModulesHelp { } {
        puts stderr "\tSets up environment for SCL rh-python36\n"
}

module-whatis   "sets up environment for SCL rh-python36"

# for Tcl script use only
set     root    /opt/rh/rh-python36/root

prepend-path	LD_LIBRARY_PATH	$root/usr/lib64
prepend-path	MANPATH		$root/usr/share/man
prepend-path	PATH		$root/usr/bin
prepend-path	PKG_CONFIG_PATH	$root/usr/lib64/pkgconfig
prepend-path	XDG_DATA_DIRS	$root/usr/share

conflict        python
```

Para acessar mais exemplos visite, https://github.com/shawfdong/modulefiles

### Referências

https://modules.readthedocs.io/en/latest/index.html
https://www.ibm.com/support/pages/using-environment-modules-manage-user-environment-platform-hpc
https://modules.sourceforge.net/
