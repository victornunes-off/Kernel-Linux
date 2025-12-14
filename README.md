# Kernel Linux Personalizado - 6.18.1

## Aluno
Beatriz Reis Dutra
Claudinei Braga de Oliveira
Douglas Santana Passos
Marcia Azevedo de Souza
Victor Gabriel Nunes de Oliveira


## Processo Realizado
1. Download dos fontes do kernel 6.18.1 (linux-6.18.1.tar.xz).
2. Configuração via `make menuconfig`, partindo da configuração padrão do Debian e desativando opções não utilizadas.
3. Compilação com `make` (sequencial) → depois interrompida e refeita com `make -j$(nproc)` para maior velocidade.
4. Instalação dos módulos (`make modules_install`) e do kernel (`make install`).
5. Geração automática do initramfs e atualização do GRUB.
6. O kernel personalizado foi instalado com sucesso em `/boot` como:
   - `vmlinuz-6.18.1`
   - `config-6.18.1`
   - `System.map-6.18.1`

## Principais Otimizações e Remoções
Foram desativadas diversas funcionalidades para deixar o kernel mais leve e focado:

### Removidos ou desativados (=n)
- Suporte completo a **Bluetooth** (drivers e stack)
- Drivers de hardware antigo/exótico (FireWire, parallel port, SCSI antigo, placas de TV, rádio, infravermelho)
- Filesystems desnecessários (NTFS, exFAT, CIFS/SMB, NFS, Ceph, ISO9660 para CDs)
- Virtualização completa (KVM, Xen) – mantido apenas suporte básico como guest
- Muitas opções de rede avançadas (WiMAX, Amateur Radio, AppleTalk, DECnet, etc.)
- Suporte a tablets/touchscreens, câmeras antigas, staging drivers
- Módulos de áudio avançados e codecs não usados
- SELinux e outras políticas de segurança avançadas
- Muitas opções de debug e profiling do kernel

### Mantidos (=y ou =m)
- Suporte completo ao hardware atual (AHCI/NVMe, Intel/AMD CPU, ext4, USB, rede Ethernet/WiFi básica)
- Initramfs, EFI, ACPI, CPU frequency scaling
- Segurança básica (assina módulos, verificação de assinatura)
- Compressão ZSTD para o kernel (mais eficiente)

### Outras configurações
- Kernel comprimido com **ZSTD** (melhor taxa de compressão)
- Preemptão voluntária (boa para desktop)
- Otimizações de compilação para performance
- Suporte a módulos mantido (a maioria dos drivers como =m)

## Resultados Esperados
- Kernel significativamente menor (vmlinuz ~10-20 MB vs ~30-40 MB do kernel padrão Debian)
- Tempo de boot mais rápido
- Menor uso de memória em idle
- Maior segurança (menos código = menor superfície de ataque)

## Arquivos Inclusos
- `config-meu-kernel-6.18.1.txt` → configuração completa usada na compilação (este é o arquivo gerado pelo `make menuconfig` e copiado de `/boot/config-6.18.1`)

O kernel está instalado e pronto para ser bootado (aparece no menu do GRUB).  
Caso queira testar, basta selecionar a entrada correspondente à versão 6.18.1.

Obrigado pela atenção!  
Qualquer dúvida sobre as escolhas de configuração, estou à disposição.
