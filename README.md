# Simulação de Ataque Mitnick (ARP Spoofing)

Este repositório contém um script em Python para simular um ataque de ARP spoofing, uma das técnicas utilizadas no famoso ataque de Kevin Mitnick.

## O Ataque

O ARP spoofing (também conhecido como ARP poisoning) é uma técnica de ataque Man-in-the-Middle (MitM) que permite a um atacante interceptar o tráfego de rede entre dois dispositivos. O atacante envia pacotes ARP falsificados para a rede local, associando seu próprio endereço MAC aos endereços IP da vítima e do roteador. Isso faz com que o tráfego da vítima para o roteador (e vice-versa) seja redirecionado através da máquina do atacante.

## Pré-requisitos

- Python 3
- Scapy

Você pode instalar o Scapy com o seguinte comando:
```bash
pip install scapy
```
ou dependendo do seu sistema:
```bash
sudo apt-get install python3-scapy
```

## Como Executar a Simulação

1.  **Identifique os IPs:** Identifique os endereços IP da sua máquina (atacante), da máquina da vítima e do roteador. Você pode usar ferramentas como `nmap` ou `ip a` para isso.

2.  **Configure o Script:** Abra o arquivo `scapy_test.py` e edite as seguintes variáveis:
    - `victim_ip`: O endereço IP da máquina vítima.
    - `router_ip`: O endereço IP do roteador (gateway).

3.  **Execute o Script:** Execute o script com privilégios de superusuário:
    ```bash
    sudo python3 scapy_test.py
    ```

## Explicação do Código

O script `scapy_test.py` usa a biblioteca Scapy para criar e enviar os pacotes ARP falsificados.

- **`victim_ip` e `router_ip`**: Definem os alvos do ataque.
- **`getmacbyip()`**: Função do Scapy que descobre o endereço MAC de um dispositivo na rede local a partir do seu IP.
- **`ARP(op=2, ...)`**: Cria um pacote de resposta ARP (`op=2`).
    - `pdst`: IP de destino.
    - `psrc`: IP de origem que o atacante quer forjar.
    - `hwdst`: MAC de destino.
- **`send()`**: Envia os pacotes para a rede.

O script envia dois pacotes:
1.  Um para a vítima, dizendo que o endereço MAC do roteador agora é o do atacante.
2.  Um para o roteador, dizendo que o endereço MAC da vítima agora é o do atacante.

## Aviso Legal

Este script é fornecido apenas para fins educacionais. O uso indevido de ferramentas de ARP spoofing em redes que você não possui ou não tem permissão para testar é ilegal. O autor não se responsabiliza pelo mau uso deste script.
