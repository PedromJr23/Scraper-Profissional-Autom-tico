# Scraper-Profissional-Autom-tico

📌 Resumo

O Scraper Profissional Automático é um sistema hospedado em servidor que coleta dados profissionais de forma automatizada utilizando Python + Selenium e a API do Google Search para localizar perfis relevantes.
Os dados coletados são enviados automaticamente para o Google Sheets (aba "resultados"), permitindo análises imediatas e integração com times de negócios.

A interface do projeto foi construída no Lovable, possibilitando disparo, visualização e acompanhamento do processamento sem necessidade de conhecimento técnico.

🎯 Objetivo

Automatizar a identificação e coleta de perfis profissionais para apoiar prospecção, inteligência comercial e pesquisas de mercado — eliminando tarefas manuais e repetitivas.

🧩 Problema

A busca manual por nomes, cargos e empresas em plataformas públicas é:

demorada

sujeita a erro

difícil de padronizar

inviável em grande volume

Isso gera perda de produtividade e gargalos para times de negócios.

🚀 Solução Desenvolvida

Um pipeline de web scraping robusto e escalável composto por:

🔹 1. API Google Search

Localiza automaticamente URLs de perfis públicos relacionados a nomes, cargos ou termos de pesquisa definidos.

🔹 2. Selenium no Servidor

Abre as URLs, extrai informações estruturadas e padroniza os dados:

Nome

Cargo

Empresa

URL do perfil

🔹 3. Google Sheets API

A base tratada é enviada diretamente para a aba “resultados”, sem intervenção humana.

🔹 4. Lovable UI

Interface intuitiva com:

Botão para disparar scraping

Campo para inserir termos de busca

Logs básicos

Indicação de status (processando / finalizado)

🏗️ Arquitetura do Pipeline
Input (Lovable) 
        ↓
API Google Search → URLs encontradas
        ↓
Selenium (Servidor) → Coleta Nome / Cargo / Empresa / Link
        ↓
Tratamento (Pandas)
        ↓
Google Sheets API → Aba "resultados"
        ↓
Interface Lovable exibe status final

🧠 Principais Funcionalidades

Busca inteligente via Google Search API

Scraping automatizado em larga escala

Coleta padronizada de informações profissionais

Execução via interface Lovable

Logs de execução

Pipeline hospedado em servidor (execução contínua/estável)

Envio automático para Google Sheets

🛠️ Tecnologias Utilizadas

Python 3

Selenium WebDriver

ChromeDriver Manager

Google Search API

gspread + Google Sheets API

Pandas

Lovable App Interface

Servidor Linux

Git/GitHub

📁 Estrutura do Repositório
/src
   /scraper
       selenium_driver.py
       parser.py
       scraper.py
   /integrations
       google_search_api.py
       sheets_service.py
   /utils
       logs.py
   /server
       run.py

README.md
requirements.txt
interface_lovable.png

from selenium import webdriver
from selenium.webdriver.common.by import By
import pandas as pd
from googleapiclient.discovery import build
import gspread

def search_profiles(query, api_key, cse_id):
    service = build("customsearch", "v1", developerKey=api_key)
    result = service.cse().list(q=query, cx=cse_id).execute()
    return [item['link'] for item in result.get('items', [])]

def extract_profile(driver, url):
    driver.get(url)

    name = driver.find_element(By.CSS_SELECTOR, ".profile-top-card-person-name").text
    cargo = driver.find_element(By.CSS_SELECTOR, ".profile-top-card__summary-item").text
    empresa = driver.find_element(By.CSS_SELECTOR, ".profile-top-card__experience-item").text

    return [name, cargo, empresa, url]
📊 Resultados Obtidos

Redução de 80% do tempo de busca manual

Coleta completamente padronizada

Dados centralizados para análises imediatas

Sistema utilizável por qualquer pessoa via interface Lovable

Pipeline replicável para outros tipos de prospecção
