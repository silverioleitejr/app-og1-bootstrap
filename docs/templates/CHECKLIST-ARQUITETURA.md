# Checklist de Arquitetura de Software Web

> **Documento:** CHECKLIST-ARQUITETURA.md  
> **Uso:** Guia de análise para a skill `sdd-adr-writer` e revisões arquiteturais.  
> **Nota:** Adaptar os itens à stack definida no `SAD.md` do projeto. Itens de stacks não utilizadas devem ser ignorados.

---

## 1. Segurança e Proteção de Dados
- [ ] Autenticação e Autorização com princípio do menor privilégio
- [ ] Criptografia em trânsito (TLS) e de dados sensíveis em repouso
- [ ] Prevenção de vulnerabilidades (injection, XSS, CSRF) via sanitização
- [ ] Gestão de segredos fora do código (variáveis de ambiente ou cofre)

## 2. Desempenho e Escalabilidade
- [ ] Arquitetura stateless para escala horizontal
- [ ] Estratégia de cache para dados frequentes
- [ ] Otimização de banco (índices, queries, réplicas quando necessário)
- [ ] Processamento assíncrono para tarefas pesadas

## 3. Disponibilidade e Resiliência
- [ ] Balanceamento de carga
- [ ] Tolerância a falhas (circuit breaker, retries com backoff)
- [ ] Backup e plano de recuperação testado

## 4. Manutenibilidade e Observabilidade
- [ ] Separação de responsabilidades em camadas
- [ ] Logs estruturados, métricas e tracing
- [ ] CI/CD com testes automatizados
- [ ] Versionamento de APIs

## 5. Privacidade
- [ ] Minimização de dados coletados
- [ ] Isolamento por usuário / tenant
- [ ] Consentimento e base legal quando aplicável
- [ ] Direito de exclusão / portabilidade considerado

---

*Checklist de referência. A skill `sdd-adr-writer` deve usá-lo como guia, não como lista rígida.*
