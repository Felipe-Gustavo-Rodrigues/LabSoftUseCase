# 🧪 Laboratório Prático: Workflow no GitHub Desktop & Resolução de Conflitos em .NET 8

Bem-vindo ao laboratório prático! 

Neste exercício, você atuará como desenvolvedor em uma **Software House**. O objetivo é simular o dia a dia de um time de desenvolvimento utilizando o **GitHub Desktop** para trabalhar com **branches**, resolver **conflitos de merge** e aplicar **hotfixes** de bugs em um projeto **.NET 8.0**.

---

## 🎯 Objetivos de Aprendizagem

- Criar um **Fork** do repositório no GitHub.
- Criar e alternar entre branches pelo **GitHub Desktop**.
- Desenvolver novas funcionalidades em branches de feature a partir da branch base `LabSofUseCase00-RevisaoGitHub`.
- Identificar e resolver **conflitos de merge** visualmente.
- Criar e integrar uma branch de **hotfix** para correção de bugs críticos em produção.

---

## 💻 Pré-requisitos

- [.NET 8 SDK](https://dotnet.microsoft.com/download/dotnet/8.0) instalado.
- [GitHub Desktop](https://desktop.github.com/) instalado e autenticado com sua conta.
- Um editor de código de sua preferência (VS Code, Visual Studio, Rider, etc.).

---

## 🚀 Etapa 0: Fork, Clone e Projeto Inicial (.NET 8)

### Step 0.1: Criar o Fork do Repositório
1. Acesse o repositório do projeto no **GitHub** pelo seu navegador.
2. No canto superior direito da página, clique no botão **Fork**.
3. Mantenha as configurações padrão e clique em **Create fork**.
4. Agora você possui uma cópia própria do repositório na sua conta do GitHub!

### Step 0.2: Clonar no GitHub Desktop
1. Abra o aplicativo **GitHub Desktop**.
2. Vá em **File > Clone Repository...** (ou `Ctrl + Shift + O`).
3. Selecione o repositório que você acabou de forkar na aba **GitHub.com**.
4. Escolha a pasta local onde deseja salvar e clique em **Clone**.

---

### Step 0.3: Código Inicial do Projeto

Verifique se a branch ativa é a `LabSofUseCase00-RevisaoGitHub`. Caso não seja:
- No **GitHub Desktop**, no topo, clique em **Current Branch** e selecione `LabSofUseCase00-RevisaoGitHub`.

Se estiver criando o código inicial na branch do projeto do zero, garanta a seguinte estrutura com dois arquivos:

#### 📄 `Tarefa.cs`
```csharp
namespace GestaoTarefas;

public class Tarefa
{
    public string Nome { get; set; } = string.Empty;
    public DateTime DataInicio { get; set; }
    public DateTime DataFim { get; set; }

    public Tarefa(string nome, DateTime dataInicio, DateTime dataFim)
    {
        Nome = nome;
        DataInicio = dataInicio;
        DataFim = dataFim;
    }

    public int ObterQuantidadeDias()
    {
        return (DataFim - DataInicio).Days;
    }
}
```

#### 📄 `Program.cs`
```csharp
using System;

namespace GestaoTarefas;

class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine("=================================");
        Console.WriteLine("   SISTEMA DE GESTÃO DE TAREFAS  ");
        Console.WriteLine("=================================\n");

        Console.Write("Digite o nome da tarefa: ");
        string nome = Console.ReadLine() ?? "Sem nome";

        Console.Write("Digite a data de início (dd/mm/aaaa): ");
        string dataInicioStr = Console.ReadLine() ?? "";
        DateTime dataInicio = DateTime.Parse(dataInicioStr);

        Console.Write("Digite a data de término (dd/mm/aaaa): ");
        string dataFimStr = Console.ReadLine() ?? "";
        DateTime dataFim = DateTime.Parse(dataFimStr);

        Tarefa tarefa = new Tarefa(nome, dataInicio, dataFim);

        Console.WriteLine("\n--- RESUMO DA TAREFA ---");
        Console.WriteLine($"Tarefa: {tarefa.Nome}");
        Console.WriteLine($"Início: {tarefa.DataInicio:dd/MM/yyyy}");
        Console.WriteLine($"Término: {tarefa.DataFim:dd/MM/yyyy}");
        Console.WriteLine($"Duração: {tarefa.ObterQuantidadeDias()} dias");
    }
}
```

> ⚠️ **Nota:** No fluxo de trabalho deste laboratório, a branch `LabSofUseCase00-RevisaoGitHub` atuará como a nossa branch principal de desenvolvimento (`develop`). Todas as novas branches devem ser criadas a partir dela e mescladas de volta para ela.

---

## 📌 Exercício 1: Implementação da RN1 (Adicionar Funcionário Responsável)

**Cenário:** O PO (Product Owner) solicitou que cada tarefa registrada agora armazene também o nome do funcionário responsável.

### 📍 Passos no GitHub Desktop & Editor:

#### Step 1.1: Criar a branch da Feature
1. No **GitHub Desktop**, garanta que em **Current Branch** esteja selecionado `LabSofUseCase00-RevisaoGitHub`.
2. Clique no menu **Current Branch** e clique no botão **New Branch**.
3. Nomeie a branch como: `feature/adicionar-funcionario`.
4. Garanta que a opção "Create branch based on `LabSofUseCase00-RevisaoGitHub`" está selecionada e clique em **Create Branch**.

#### Step 1.2: Atualizar os Arquivos no seu Editor de Código

##### Modifique o arquivo `Tarefa.cs`:
```csharp
namespace GestaoTarefas;

public class Tarefa
{
    public string Nome { get; set; } = string.Empty;
    public string NomeFuncionario { get; set; } = string.Empty; // RN1: Novo campo
    public DateTime DataInicio { get; set; }
    public DateTime DataFim { get; set; }

    public Tarefa(string nome, string nomeFuncionario, DateTime dataInicio, DateTime dataFim)
    {
        Nome = nome;
        NomeFuncionario = nomeFuncionario;
        DataInicio = dataInicio;
        DataFim = dataFim;
    }

    public int ObterQuantidadeDias()
    {
        return (DataFim - DataInicio).Days;
    }
}
```

##### Modifique o arquivo `Program.cs`:
```csharp
using System;

namespace GestaoTarefas;

class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine("=================================");
        Console.WriteLine("   SISTEMA DE GESTÃO DE TAREFAS  ");
        Console.WriteLine("=================================\n");

        Console.Write("Digite o nome da tarefa: ");
        string nome = Console.ReadLine() ?? "Sem nome";

        Console.Write("Digite o nome do funcionário responsável: ");
        string funcionario = Console.ReadLine() ?? "Não informado";

        Console.Write("Digite a data de início (dd/mm/aaaa): ");
        string dataInicioStr = Console.ReadLine() ?? "";
        DateTime dataInicio = DateTime.Parse(dataInicioStr);

        Console.Write("Digite a data de término (dd/mm/aaaa): ");
        string dataFimStr = Console.ReadLine() ?? "";
        DateTime dataFim = DateTime.Parse(dataFimStr);

        Tarefa tarefa = new Tarefa(nome, funcionario, dataInicio, dataFim);

        Console.WriteLine("\n--- RESUMO DA TAREFA ---");
        Console.WriteLine($"Tarefa: {tarefa.Nome}");
        Console.WriteLine($"Responsável: {tarefa.NomeFuncionario}");
        Console.WriteLine($"Início: {tarefa.DataInicio:dd/MM/yyyy}");
        Console.WriteLine($"Término: {tarefa.DataFim:dd/MM/yyyy}");
        Console.WriteLine($"Duração: {tarefa.ObterQuantidadeDias()} dias");
    }
}
```

#### Step 1.3: Commitar e Fazer Merge na Branch Base pelo GitHub Desktop

1. Volte ao **GitHub Desktop**. Você verá as alterações listadas na barra lateral esquerda.
2. No campo **Summary (required)** no canto inferior esquerdo, digite:
   `feat(tarefa): adiciona campo NomeFuncionario`
3. Clique em **Commit to feature/adicionar-funcionario**.
4. Troque para a branch principal de desenvolvimento: clique em **Current Branch** e selecione `LabSofUseCase00-RevisaoGitHub`.
5. No menu superior do GitHub Desktop, vá em **Branch > Merge into current branch...**.
6. Selecione `feature/adicionar-funcionario` na lista e clique no botão **Merge feature/adicionar-funcionario into LabSofUseCase00-RevisaoGitHub**.
7. Clique em **Push origin** no topo para enviar as atualizações ao seu GitHub.

---

## ⚡ Exercício 2: Mudanças de Usabilidade e Conflito de Merge (RN2A e RN2B)

**Cenário:** Vamos simular dois desenvolvedores alterando a mesma linha do título no arquivo `Program.cs` ao mesmo tempo. Isso vai gerar um **conflito de merge**, que você aprenderá a resolver facilmente!

---

### 🟢 Parte A: RN2A - Adicionar Versão no Título

#### Step 2A.1: Criar a branch `feature/titulo-versao`
1. No **GitHub Desktop**, altere a **Current Branch** para `LabSofUseCase00-RevisaoGitHub`.
2. Clique em **Current Branch > New Branch**.
3. Digite o nome `feature/titulo-versao` (baseada em `LabSofUseCase00-RevisaoGitHub`) e clique em **Create Branch**.

#### Step 2A.2: Alterar o código
Abra o arquivo `Program.cs` e edite o título do console para incluir a versão:

```csharp
// Em Program.cs, modifique o bloco do cabeçalho:
Console.WriteLine("=================================");
Console.WriteLine(" SISTEMA DE GESTÃO DE TAREFAS - Versão 1.0.0");
Console.WriteLine("=================================\n");
```

#### Step 2A.3: Commitar e fazer Merge
1. No **GitHub Desktop**, faça o commit com a mensagem: `feat(usabilidade): adiciona versao 1.0.0 no titulo`.
2. Alterne a **Current Branch** de volta para `LabSofUseCase00-RevisaoGitHub`.
3. Vá no menu **Branch > Merge into current branch...**.
4. Selecione `feature/titulo-versao` e clique em **Merge**.

---

### 🔵 Parte B: RN2B - Adicionar Nome da Empresa no Título

#### Step 2B.1: Criar a branch `feature/titulo-softwarehouse`
1. Garanta que você voltou para a branch `LabSofUseCase00-RevisaoGitHub`.
2. Clique em **Current Branch > New Branch**.
3. Digite o nome `feature/titulo-softwarehouse` (baseada em `LabSofUseCase00-RevisaoGitHub`) e clique em **Create Branch**.

#### Step 2B.2: Alterar o código
Abra o arquivo `Program.cs` e modifique a linha do título adicionando o nome da empresa:

```csharp
// Em Program.cs, modifique o bloco do cabeçalho:
Console.WriteLine("=================================");
Console.WriteLine(" SoftwareHouse - SISTEMA DE GESTÃO DE TAREFAS");
Console.WriteLine("=================================\n");
```

#### Step 2B.3: Commitar e tentar fazer o Merge
1. No **GitHub Desktop**, faça o commit com a mensagem: `feat(usabilidade): adiciona marca da SoftwareHouse no titulo`.
2. Alterne a **Current Branch** de volta para `LabSofUseCase00-RevisaoGitHub`.
3. Vá no menu **Branch > Merge into current branch...**.
4. Selecione `feature/titulo-softwarehouse` e clique em **Merge**.

💥 **CONFLITO DETECTADO!** 💥

O GitHub Desktop exibirá um aviso informando que há **1 conflito de arquivo** em `Program.cs` e não pode fazer o merge automático.

---

### 🛠️ Parte C: Resolução do Conflito de Merge

1. No próprio aviso de conflito do **GitHub Desktop**, clique na opção **Open in Visual Studio Code** (ou no seu editor configurado).
2. O editor exibirá as marcações de conflito no código:

```csharp
<<<<<<< HEAD
Console.WriteLine(" SISTEMA DE GESTÃO DE TAREFAS - Versão 1.0.0");
=======
Console.WriteLine(" SoftwareHouse - SISTEMA DE GESTÃO DE TAREFAS");
>>>>>>> feature/titulo-softwarehouse
```

3. **Como resolver:**
   - Unifique ambas as alterações para manter tanto o nome da empresa quanto a versão:
   ```csharp
   Console.WriteLine("=================================");
   Console.WriteLine(" SoftwareHouse - SISTEMA DE GESTÃO DE TAREFAS - Versão 1.0.0");
   Console.WriteLine("=================================\n");
   ```
   - Remova completamente as marcações do Git (`<<<<<<<`, `=======`, `>>>>>>>`).
   - Salve o arquivo (`Ctrl + S`).

4. Volte ao **GitHub Desktop**:
   - O programa detectará automaticamente que o conflito foi resolvido.
   - Clique no botão **Commit merge**.
   - Clique em **Push origin** para atualizar o seu repositório remoto.

---

## 🐛 Exercício 3: Resolução de Bug Critical (Hotfix de Formato de Data)

**Cenário de Produção:** Os usuários relataram que o programa fecha sozinho (**crash**) quando a data é digitada com espaços, letras ou em formatos diferentes do esperado. 

Precisamos criar urgentemente uma branch `hotfix/formatoData` para tratar essa exceção usando `DateTime.TryParseExact` e garantir que o programa peça para o usuário digitar a data novamente caso esteja em formato inválido.

---

### 📍 Passos para a Solução:

#### Step 3.1: Criar a branch de Hotfix
1. No **GitHub Desktop**, certifique-se de estar na branch `LabSofUseCase00-RevisaoGitHub`.
2. Clique em **Current Branch > New Branch**.
3. Nomeie a nova branch como: `hotfix/formatoData`.
4. Clique em **Create Branch**.

#### Step 3.2: Atualizar `Program.cs` no Editor
Abra o arquivo `Program.cs` e implemente a validação de data com método auxiliar:

```csharp
using System;
using System.Globalization;

namespace GestaoTarefas;

class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine("=================================");
        Console.WriteLine(" SoftwareHouse - SISTEMA DE GESTÃO DE TAREFAS - Versão 1.0.0");
        Console.WriteLine("=================================\n");

        Console.Write("Digite o nome da tarefa: ");
        string nome = Console.ReadLine() ?? "Sem nome";

        Console.Write("Digite o nome do funcionário responsável: ");
        string funcionario = Console.ReadLine() ?? "Não informado";

        DateTime dataInicio = LerDataValida("Digite a data de início (dd/mm/aaaa): ");
        DateTime dataFim = LerDataValida("Digite a data de término (dd/mm/aaaa): ");

        while (dataFim < dataInicio)
        {
            Console.WriteLine("\n⚠️ Ops! A data de término não pode ser anterior à data de início.");
            dataFim = LerDataValida("Digite novamente a data de término (dd/mm/aaaa): ");
        }

        Tarefa tarefa = new Tarefa(nome, funcionario, dataInicio, dataFim);

        Console.WriteLine("\n--- RESUMO DA TAREFA ---");
        Console.WriteLine($"Tarefa: {tarefa.Nome}");
        Console.WriteLine($"Responsável: {tarefa.NomeFuncionario}");
        Console.WriteLine($"Início: {tarefa.DataInicio:dd/MM/yyyy}");
        Console.WriteLine($"Término: {tarefa.DataFim:dd/MM/yyyy}");
        Console.WriteLine($"Duração: {tarefa.ObterQuantidadeDias()} dias");
    }

    /// <summary>
    /// Método auxiliar para ler e validar a data digitada pelo usuário.
    /// Evita crashes do sistema ao passar formatos incorretos.
    /// </summary>
    private static DateTime LerDataValida(string mensagemPrompt)
    {
        DateTime dataResultado;
        string[] formatosAceitos = { "dd/MM/yyyy", "d/M/yyyy" };

        while (true)
        {
            Console.Write(mensagemPrompt);
            string entrada = Console.ReadLine() ?? "";

            if (DateTime.TryParseExact(entrada, formatosAceitos, CultureInfo.InvariantCulture, DateTimeStyles.None, out dataResultado))
            {
                return dataResultado;
            }

            Console.WriteLine("❌ Data em formato inválido! Por favor utilize o formato dd/mm/aaaa (Ex: 25/12/2024).\n");
        }
    }
}
```

#### Step 3.3: Commitar e Integrar o Hotfix
1. No **GitHub Desktop**, faça o commit das alterações:
   - Summary: `fix(hotfix): adiciona validacao TryParseExact para evitar crash na digitação de datas`
2. Clique em **Commit to hotfix/formatoData**.
3. Alterne a **Current Branch** para `LabSofUseCase00-RevisaoGitHub`.
4. Vá no menu **Branch > Merge into current branch...**.
5. Escolha `hotfix/formatoData` e confirme o merge clicando em **Merge**.
6. Clique em **Push origin** para enviar a versão final com o bug corrigido para o seu GitHub!

---

## 🏆 Resumo das Ações Realizadas no GitHub Desktop

| Objetivo | O que foi feito no GitHub Desktop |
| :--- | :--- |
| **Criar Fork** | Feito no site do GitHub e clonado no GitHub Desktop via `File > Clone Repository` |
| **Criar Branches** | Selecionado `Current Branch > New Branch` a partir da branch base `LabSofUseCase00-RevisaoGitHub` |
| **Salvar Alterações** | Preenchido o `Summary` e clicado em `Commit to <branch>` |
| **Mesclar Código** | Selecionado `Branch > Merge into current branch...` estando na branch principal |
| **Resolver Conflito** | Editado o código diretamente no editor ao tentar fazer o merge, e confirmado via `Commit merge` |
| **Sincronizar** | Clicado em `Push origin` no topo da janela |

---

## 🎉 Parabéns!

Você concluiu a prática laboratorial utilizando **GitHub Desktop**! Agora você sabe como trabalhar com forks, gerenciar branches visivelmente, solucionar conflitos de merge e aplicar hotfixes em projetos .NET 8.
