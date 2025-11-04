# aws-ec2-webserver-lab
Documentação de laboratório prático focado no deploy, monitoramento e redimensionamento seguro de um servidor web Apache (httpd) utilizando Amazon EC2.


# AWS EC2 Lab - Deploy e Gestão de um Servidor Web

**Autor:** Lucas Moreira de Araujo

**Contexto:** Documentação da execução prática do laboratório "Introduction to Amazon EC2", com foco em segurança, automação e escalabilidade.

---

## Objetivo Principal

Este laboratório prático focou no deploy eficiente de um servidor web Apache (`httpd`) na nuvem, utilizando uma instância **Amazon EC2**. O objetivo foi ir além da simples inicialização, explorando *best practices* como automação via User Data, controle granular de tráfego via Security Group e gestão do ciclo de vida da instância (redimensionamento e proteção contra encerramento).

## Etapas e Destaques Técnicos

O projeto foi dividido nas seguintes fases, com aprendizados técnicos cruciais em cada uma:

### 1. Provisionamento e Automação Inicial

* **Instância Base:** Seleção da AMI **Amazon Linux 2023** e tipo de instância `t3.micro`.
* **User Data Script:** Utilizei o campo **User Data** para automatizar a configuração do servidor na primeira inicialização. Isso garante que a instância já suba pronta para servir conteúdo.

**Arquivo: `user_data_script.sh`**

```bash
#!/bin/bash
yum -y install httpd
systemctl enable httpd
systemctl start httpd
echo '<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>EC2 Web Server by Lucas Moreira</title>
  <style>
    body { 
      font-family: "Segoe UI", Arial, sans-serif; 
      background-color: #0d1117; 
      color: #00ffa2; 
      text-align: center; 
      margin-top: 10%;
    }
    h1 { font-size: 2.5rem; margin-bottom: 0.5rem; }
    p { color: #b0b0b0; font-size: 1rem; }
    .credit { margin-top: 2rem; font-size: 0.9rem; color: #666; }
  </style>
</head>
<body>
  <h1>🚀 Welcome to My AWS EC2 Web Server</h1>
  <p>Instance running on Amazon Linux — automatically configured via User Data.</p>
  <div class="credit">Developed by <strong>Lucas Moreira</strong></div>
</body>
</html>' > /var/www/html/index.html
