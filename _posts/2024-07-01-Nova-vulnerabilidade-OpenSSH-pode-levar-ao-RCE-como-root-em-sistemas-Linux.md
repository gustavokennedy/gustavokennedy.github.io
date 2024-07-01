# Nova vulnerabilidade OpenSSH pode levar ao RCE como root em sistemas Linux

Os mantenedores do OpenSSH lançaram atualizações de segurança para conter uma falha crítica de segurança que pode resultar na execução remota de código não autenticado com privilégios de root em sistemas Linux baseados em glibc.

A vulnerabilidade, codinome regreSSHion, recebeu o identificador CVE CVE-2024-6387. Ela reside no componente do servidor OpenSSH, também conhecido como sshd, que é projetado para escutar conexões de qualquer um dos aplicativos clientes.

"A vulnerabilidade, que é uma condição de corrida do manipulador de sinais no servidor do OpenSSH (sshd), permite execução remota de código (RCE) não autenticada como root em sistemas Linux baseados em glibc", disse Bharat Jogi, diretor sênior da unidade de pesquisa de ameaças da Qualys, em uma divulgação publicada hoje. "Essa condição de corrida afeta o sshd em sua configuração padrão."

A empresa de segurança cibernética disse ter identificado nada menos que 14 milhões de instâncias de servidores OpenSSH potencialmente vulneráveis ​​expostas à internet, acrescentando que se trata de uma regressão de uma falha de 18 anos já corrigida, rastreada como CVE-2006-5051 , com o problema restabelecido em outubro de 2020 como parte da versão 8.5p1 do OpenSSH.

"A exploração bem-sucedida foi demonstrada em sistemas Linux/glibc de 32 bits com [ randomização do layout do espaço de endereço ]", disse o OpenSSH em um aviso. "Em condições de laboratório, o ataque requer em média 6-8 horas de conexões contínuas até o máximo que o servidor aceitará."

A vulnerabilidade afeta versões entre 8.5p1 e 9.7p1. Versões anteriores a 4.4p1 também são vulneráveis ​​ao bug de condição de corrida, a menos que sejam corrigidas para CVE-2006-5051 e CVE-2008-4109 . Vale a pena notar que os sistemas OpenBSD não são afetados, pois incluem um mecanismo de segurança que bloqueia a falha.

É provável que a falha de segurança também afete o macOS e o Windows, embora sua explorabilidade nessas plataformas ainda não tenha sido confirmada e exija mais análises.
Especificamente, a Qualys descobriu que se um cliente não for autenticado em 120 segundos (uma configuração definida pelo LoginGraceTime), o manipulador SIGALRM do sshd será chamado de forma assíncrona, de uma maneira que não é segura para sinais assíncronos.

O efeito líquido da exploração do CVE-2024-6387 é o comprometimento e a tomada de controle de todo o sistema, permitindo que agentes de ameaças executem códigos arbitrários com os mais altos privilégios, subvertam mecanismos de segurança, roubem dados e até mesmo mantenham acesso persistente.

"Uma falha, uma vez corrigida, reapareceu em uma versão de software subsequente, normalmente devido a alterações ou atualizações que inadvertidamente reintroduzem o problema", disse Jogi. "Este incidente destaca o papel crucial de testes de regressão completos para evitar a reintrodução de vulnerabilidades conhecidas no ambiente."

Embora a vulnerabilidade tenha obstáculos significativos devido à sua natureza de condição de corrida remota, os usuários são recomendados a aplicar os patches mais recentes para se protegerem contra ameaças potenciais. Também é aconselhável limitar o acesso SSH por meio de controles baseados em rede e impor segmentação de rede para restringir acesso não autorizado e movimento lateral.
