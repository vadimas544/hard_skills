1. CVS(control version system) - GIT(basic usage).
2. Work with HTTP Protocol(debug(telnet, curl, chrome dev tools), Request, Response, statuses), FTP, SFTP(WinSCP, MC, TotalCommander),
SSH Connections(PuTTy, SSH-Keygens, SSH Keys), SCP(copying files from/to local/remote comuter).And OSI model Protocols.
3. Basic terminal usage(all comands for everyday usage).
4. Work with tasktrackers(basic).
5. Work with timetrackers(for every task).
6. Most basic data structures and algirythms.
7. Basic configuration and work with PHPStorm.
8. Basic English language.

1.GIT
git version - check version
git config --global user.name "Vadim Samoilenko - set user name
git config --global user.email "vadim123544@gmail.com" - set user email
git config --unset-all --global user.email - delete user.email
git config --list - check all settings

git init - initialize empty git project(only in folder with project), creating hidden folder .git(all diffs and configs).
git status - check what files and what type of stage of this files(stage, tracked, untracked, modify).
git add file - add file to stage area(we only add file, but don`t track him)
git reset HEAD file - delete file in stage area
git rm file.txt - remove file
git reset --hard - discard changes to first commit
git reset --id_of_commit - discard changes to this commit
git add . - add all files to stage area
git commit -m "message" - save snapshot of changes in files(now we have id of snaphot)
git commit --amend --no-edit - add changes into last commit without changing comment
git commit --amend -m "New message" - add changes into last commit with changing comment
git checkout --file.txt - reset changes in this file
git checkout id(last 4 numbers) - move to this commit
HEAD - current pointer(current active branch), master - current branch, origin - remote repo(by default)
git branch - list of branches
git branch -va - info about branches
git branch new_feature - create branch new_feature
git branch --delete local_branch
git checkout new_feature - change branch to new_feature
git commit -m "Message for new_feature branch" - save snapshot of changes in new_feature branch
git checkout master - move to master branch
git merge new_feature - merge our changes in new_feature branch into master(fast-forward merge, without conflicts, if
	we have conflicts(we edit files in master branch) we must manually fix all changes in both files).
git merge --abort - reset last merge
git stash - a big buffer(when we move to other branch we must commit all our changes, but work in this branch not done, there we add all this files in buffer).
git stash list - list buffer content
git stash pop - extract all buffer content
git log - history of commits
git clone url . - copy files from remote repo and connect this repo for remote work with him
git remote add repo_name url - connect remote repo to this git project
git remote -av - check all remote repos
git remote remove remote_repo - delete remote repo
git push remote_repo local_branch - send changes to remote repo
git push --set-upstream origin local_branch - send local branch to remote repo
git fetch remote_repo - get all changes from remote repo to local
git pull remote_repo local_branch - add remote repo, and fetch all data from remote repo
git tag - tagging commit or branch
.gitignore - special file where we ignore(not track with git) all this files and dirs.
Work with Github(pull request, fork)!!! 
pull request - we can accept all changes that we done in our local repo or decline(this changes accept the main developer)
fork - this is copy of that project what we fork
In root directory of our project we need create readme.md(we must descrpipt our project)
connect to remote repo with ssh(keygens).


2. WORK WITH HTTP PROTOCOL

Network for junior
HTTP - hypertext transfer protocol(protocol without saving state, without connection establish).
Have two phase(HTTP Request and HTTP Response).
Request: 
	Method:  GET /google.com/index.php HTTP/1.1 /n
	Headers: Cache-Control, Host, ... /n
	Body From user /n/n
Response:
	Method: HTTP/1.1 200OK /n
	Headers: From Server
	Body: content from server

HTTP Protocol have many statuses:
100... - informational
200... - success statuses
300... - Redirection
400... - client error(forbidden, not found, access)
500... - server error

HTTP Methods: 
GET, HEAD - get data from server, in HEAD only headers
POST(send data to the server), PUT(replace data with this content), DELETE(remove on server with this content), PATCH(partial change of resource) - modify data on server(insert, update, delete).
CONNECT(establish a tunnel with URI), OPTIONS(describe a communication options for the resource), TRACE(loopback info for target resource) - debug methods

If we want to save permament connection with server use WebSockects.
At first connection to a server, he send headers that say use WebSockets
Comet - technology, that describe some techics for get data from server(pulling, server push, long pulling).
Pulling - request to server for some data, who changes periodically(currency, aukzion, ...).
Server push - server tell us, if something change on server.
Long pulling - send request to a server, and if he has data, he take us, but if no, he take connection open.


To connect on other machine in network or to check open port we have telnet.This is a protocol who check port 
and all data send in opened wiew.
telnet google.com 443 - establish connection or no

To check accessing to site we use curl(libraries for work with url(download files, send files on server, etc...)):
curl -Is http://google.com | head -n 1 or
curl -Is http://google.com - return only headers or 
curl http://google.com - return main page

Or we can check the site with wget(linux utilite to downloading of)
wget -O file http://google.com - the content of google.com/index.php we send to file

Also we have Chrome Dev tools to debug site:
	Elements
		To check the element use cursor in rectangle
		We can edit text inside tags, and edit tags
		we can add attribute, and edit attribute
		we can delete element, and copy element and paste element
		If we dont know how to use this element in CSS, we can copy selector!!!
		We can hide element
		We can change a state of element: active, hover, focus, visisted...
		If we want to debug a javascript code that contains in some html, we 
		check subtree breakpoint, and if we clicked we got to a source and js file and js line
	Console
		In Elements what we choose we use $0
		In console we can talk with this current element - alert($0.innerHTML)
		console.log, console.info - the white color of console
		console.warn - yellow, console.error - red
		In console we can run JS code

FTP access we have into WinSCP and MC, or TotalCommander

SSH connection we use into Putty or openssh client on Linux
ssh username@185.25.116.77 - open connection
If we want connect always to remote server we need generate ssh keys.In local machine:
ssh-keygen -b 4096 - we genarate in /home/vadim/.ssh/ two keys public and private
Now we need upload public key into a server /home/root(user that we connect to a server)/.ssh/authorized_keys and give that permissions:
ssh your_username@192.0.2.0 - connect to a server
mkdir -p ~/.ssh && touch ~/.ssh/authorized_keys - create a folder structure
chmod 700 ~/.ssh && chmod 600 ~/.ssh/authorized_keys - give permissions
scp ~/.ssh/id_rsa.pub your_username@192.0.2.0:~/.ssh/authorized_keys - copy a public key into server

SCP commands for copy files:
scp user@remote.host:file.txt /some/local/directory - copy file.txt from remote to local
scp file.txt user@remote.host:/some/remote/directory - copy file.txt from local to remote
scp -r dir1 user@remote.host:/some/remote/directory/dir2 - copy dir1 from local to remote folder dir2
scp user@remote.host1:/directory/file.txt user@remote.host2:/some/directory/ - copy file.txt from one remote server to another
scp file1.txt file2.txt user@remote.host:~ - copy some files to remote server
scp -P 2222 file.txt user@remote.host:/some/remote/directory - copy file.txt to remote server into port 2222

openssh, openssh-server - packages for ssh

OSI Model
1. Physical - bits, bytes, signals
2. Data Link - frames, MAC(Media Accesss Control) addresses, LLC(Logical Link Control)
Data Link layer is handled by the NIC (Network Interface Card) and device drivers of host machines.
Switch & Bridge are Data Link Layer devices.
3. Network Layer(IP, ICMP, NAT, ARP)
Routing: The network layer protocols determine which route is suitable from source to destination. This function of network layer is known as routing.
Logical Addressing: In order to identify each device on internetwork uniquely, network layer defines an addressing scheme. The sender & receiver’s IP address are placed in the header by network layer. Such an address distinguishes each device uniquely and universally
Segment in Network layer is referred as Packet.
Network layer is implemented by networking devices such as routers.
4. Transport Layer(TCP(protocol with ), UDP).
Transport layer provides services to application layer and takes services from network layer. The data in the transport layer is referred to as Segments.
In TCP Protocol if we lost data we rerequest data(segments).
In UDP Protocol we can loose the data(datagramms).
TCP Ports(1-65535), and 1-1024 reserved for system services.
PHP work only with TCP level(sockets) and higher.
5. Session Layer(TLS, SSL)
6. Presentation Layer also called Translation layer.
Translation : For example, ASCII to EBCDIC.
Encryption/ Decryption : Data encryption translates the data into another form or code. The encrypted data is known as the cipher text and the decrypted data is known as plain text. A key value is used for encrypting as well as decrypting data.
Compression: Reduces the number of bits that need to be transmitted on the network.
7. Application Layer (HTTP, FTP. SMTP, SSH, DNS, ...).


TCP/IP Model:
1. Data Link(physical and data link layers).
2. Network Layer.
3. Transport Layer.
4. Application Layer(include session, presentation, and application layers).


3. BASIC TERMIMAL USAGE

cd, ls, echo Hi > file.txt, cat, less, nano, vim, pwd, touch, cp -R, mv, man, info, history, which, whereis
mkdir, rmdir, rm, gzip, bzip, tar, top, netstat, ps, systemctl start(stop, status) services, grep, ln, chmod, chown, find, du -h, df -h,   
CTRL+L(clear),CTRL+A(begin of text), CTRL+E(end of text).  

4. WORK WITH TASKTRAKERS

ToDoList for Windows is the best solution.

5. WORK WITH TIMETRACKERS

Toggl the best solution

6. Most basic data structures and algirythms.

In PHP we have SPL(Standart PHP Library) where we have structures, iterators, exceptions and functions for work with many
structures of data without including external libraries.
Structure of data - this is a programm unit, that can save and proceed many data of the same type or who have logical connections.

Some basic structures:
List(односвязный, двусвязный)
Tree(binary tree, heap, nested sets)

Односвязный список - состоит из узлов, каждый из которых содержит данные, так и/или ссылки на следующий и предыдущий узлы.
Двухзвязный список - в каждом узле даного списка есть ссылки на предыдущий и последующий узел. Удобно передвигаться в любом направлении,
просто удаление и перестановка елементов. Основа для стэка и очереди.Все операции имеют низкую алгоритмическую сложность.

СТЭК - абстрактный тип данных, органнизованный по принципу LIFO(last in first out).Последним зашел - первым вышел. Как в стакане, или рожок автомата.
Очередь - абстрактный тип данных, органнизованный по принципу FIFO(first in first out).
Куча - деревовидная структура(граф)б каждый узел больше или равен своим потомкам.

$stack = new SplStack(); - create object of stack

$stack->push('1');
$stack->push('2');
$stack->push('3');

И если извлечь, то первым выйдет 3.

$queue = new SplQueue();
$queue->enqeue('one'); - поставить в очередь
$queue->enqeue('two');
$queue->enqeue('three');

SplHeap - abstract class for Heap, but we have two childs SplMaxHeap(range by max), SplMinHeap(range by min).insert(), extract() - operations for heap.
SplPriorityQueue - queue with priority.

Array in SPL
In Zend Engine array is a HashTable with pointers to (first value, last value, current value, array of references, containers for references).

In PHP SPL we have classic massive(numerical massive with fixed number of elements, work fast than simple array).
When we work with foreach we create a copy of array and than proceed every element.
When we work with iterators we don`t create a copy, we work with this massive.

Итератор - это интерфейс, предоставляющий доступ к элементам коллекции(массива или контейнера) и навигацию по ним.

Обход директорий например лучше сделать итератором

$dir = new DirectoryIterator("/dir");

foreach( $dir as $item) {
	echo $item . '<br />';
}

Можно посмотреть список интерфейсов, родительских классов, трейтов, кол-во элементов, spl_autoload - это все прелести SPL.

7. Basic configuration and work with PHPStorm.

- run PHPStorm
- install theme;
- install font for workspace;
- hide all toolbars(view - uncheck all);