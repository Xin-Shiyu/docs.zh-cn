---
title: 云本机 DevOps
description: 构建适用于 Azure 的云本机 .NET 应用 |云本机 DevOps
ms.date: 06/30/2019
ms.openlocfilehash: 2b3dd47eeeb69d63f5ae39705abb9d1d51295645
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2019
ms.locfileid: "73841815"
---
# <a name="cloud-native-devops"></a>云本机 DevOps

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

软件顾问最喜爱的口头禅是解答 "这一问题，它取决于所提出的任何问题。 这并不是因为软件顾问喜欢不是一个位置。 这是因为软件中的任何问题都没有真正的答案。 没有绝对权限和错误，而是相对之间的平衡。

例如，开发 web 应用程序的两个主要方面：单页面应用程序（Spa）与服务器端应用程序。 一方面，用户体验会更好地用于 Spa，可以最大程度地减少到 web 服务器的流量，使其能够在与静态宿主简单的操作上托管。 另一方面，Spa 往往会变慢，并且更难测试。 哪一个是正确的选择？ 这取决于你的情况。

云本机应用程序不会受到相同分裂的不受限于。 它们在开发、稳定性和可伸缩性方面具有明显的优势，但对它们进行管理可能有点困难。

几年前，将应用程序从开发环境转移到生产环境的过程要花一个月，甚至更多。 公司在6个月甚至每年的步调上发布软件。 在 Windows 10 之前的那一天之前，只需要查看 Microsoft Windows，才能获得可接受的发布节奏。 五年在 Windows XP 和 Vista 之间传递，在 Vista 和 Windows 7 之间还有3个。

它现在相当明确，能够发布软件，使快速发展的公司在 sloth 的竞争对手更具优势。 这是因为，Windows 10 的主要更新现在大约每六个月执行一次。

支持更快速、更可靠的版本实现业务价值的模式和实践统称为 "DevOps"。 它们包括从整个软件开发生命周期到整个软件开发生命周期的各种创意，从指定应用程序一直到提供和操作该应用程序。

DevOps 在微服务之前发生，并且很可能会更小，更适合使用目的服务，无需进行发布和操作，而只是在生产中运行的应用程序更简单。

![图11-0 搜索趋势表明，微服务的增长不会开始，DevOps 是一种非常合理的理念。](./media/microservices-vs-devops.png)

通过良好的 DevOps 实践，可以实现云本机应用程序的优势，而无需 suffocating 的工作实际运行应用程序。

DevOps 时，不会有任何黄金 hammer。 任何人都不能销售完整且全面的解决方案，用于发布和运行高质量的应用程序。 这是因为每个应用程序与其他应用程序完全不同。 不过，有一些工具可以使 DevOps 的意义更少。 其中一种工具称为 Azure DevOps。

## <a name="azure-devops"></a>Azure DevOps

Azure DevOps 的 pedigree 较长。 当 Team Foundation Server 首次移动并通过各种名称更改： Visual Studio Online 和 Visual Studio Team Services 时，它可以将其根追溯回。 不过，多年来，它远远超出了其前置任务。

Azure DevOps 分为五个主要组件：

![图 11-1 Azure DevOps 的五个主要区域](./media/devops-components.png)

**Azure Boards** -提供一个问题和工作项跟踪工具，旨在允许用户选择最适合自己的工作流。 它附带多个预先配置的模板，其中包括用于支持 SCRUM 和看板开发样式的模板。

**Azure Repos**源代码管理，支持古老 TEAM FOUNDATION 版本控制（TFVC）和业界喜爱的 git。 拉取请求提供了一种方法来实现社交编码，方法是在进行更改时对其进行讨论。

**Azure Pipelines** -支持与 Azure 紧密集成的生成和发布管理系统。 可从 Windows 到 Linux 的各种平台上运行生成到 MacOS。 可以在云中或本地预配生成代理。

**Azure Test Plans** -通过 Test Plans 功能提供的测试管理和探索性测试支持，不会留下 QA 人员。

**Azure Artifacts** -一个项目源，允许公司创建其自己的、内部、版本的 NuGet、npm 和其他版本。 如果集中式存储库出现故障，则该服务可充当上游包的缓存。

Azure DevOps 中的顶层组织单位称为 "项目"。 在每个项目中，可以打开和关闭各种组件，如 Azure Artifacts。 如果用户想要管理其在 GitHub 中的源代码，但仍要利用 Azure Pipelines，则这是完全可能的。 事实上，许多开源项目都利用了 Azure DevOps 提供的[免费版本](https://azure.microsoft.com/blog/announcing-azure-pipelines-with-unlimited-ci-cd-minutes-for-open-source/)，同时在 GitHub 上保留源代码。 一些重要的开源项目（如[Visual Studio Code](https://code.visualstudio.com/)、 [yarn](https://yarnpkg.com/en/)、 [gulp](https://gulpjs.com/)和[NumPy](https://www.numpy.org/) ）进行了转换。

其中每个组件都为云本机应用程序提供了一些优势，但最有用的三个组件是源代码管理、板和管道。  

## <a name="source-control"></a>源代码管理

组织云本机应用程序的代码可能会很困难。 云本机应用程序不是单个非常大的应用程序，而是由相互之间相互通信的小型应用程序构成。 与计算中的所有情况一样，代码的最佳排列仍是一个开放式问题。 使用不同种类的布局时，有成功的应用程序示例，但两个变体看起来最受欢迎。

在开始实际源控件之前，可能需要决定适当的项目数量。 在单个项目中，支持多个存储库，并生成管道。 板稍微复杂一些，但可以轻松地将任务分配给单个项目中的多个团队。 当然，可以支持数百个甚至数千个开发人员，而不是单个 Azure DevOps 项目。 这样做可能是最佳方法，因为它为所有开发人员提供了一个单一位置，并减少了开发人员不确定应用程序所驻留的项目时发现该应用程序的混乱程度。

将微服务的代码拆分到 Azure DevOps 项目中可能会稍微提高难度。

![图11-2 单个和多个存储库](./media/single-repository-vs-multiple.png)

### <a name="repository-per-microservice"></a>每微服务的存储库

乍一看，这似乎是拆分微服务的源代码的最逻辑方法。 每个存储库可以包含生成一个微服务所需的代码。 此方法的优点非常明显：

1. 有关生成和维护应用程序的说明可以添加到每个存储库根目录中的自述文件。 在浏览存储库时，可以轻松地找到这些说明，缩短开发人员的加速时间。
2. 每个服务都位于一个逻辑位置，可通过了解服务的名称轻松找到。
3. 可以轻松地设置生成，以便仅当对所属存储库进行更改时才触发生成。
4. 进入存储库中的更改数量仅限于处理此项目的少数开发人员。
5. 通过限制开发人员拥有读取和写入权限的存储库，可以轻松地设置安全性。
6. 所有者组可以更改存储库级别设置，最少与其他人进行讨论。

微服务背后的一项重要想法是，服务应该是孤立的，彼此之间是分离的。 当使用域驱动设计来决定服务的边界时，服务将充当事务边界。 数据库更新不应跨多个服务。 此相关数据的集合称为 "边界上下文"。  这一想法通过将微服务数据隔离到独立的数据库，与服务的其余部分分开。 通过这种方式，您可以很好地将此理念传递到源代码。

但是，这种方法没有什么问题。 我们的时间 gnarly 的开发问题之一就是管理依赖项。 考虑构成平均 `node_modules` 目录的文件数。 全新安装的内容（如 `create-react-app`）可能会引入上千个包。 如何管理这些依赖项的问题是一项困难的问题。

如果更新了依赖项，则下游包还必须更新此依赖项。 遗憾的是，这种情况下，使用开发工作会使 `node_modules` 目录最终出现在单个包的多个版本中，每个版本都是以略微不同的步调版本化的其他某个包的依赖项。 部署应用程序时，应使用哪种版本的依赖项？ 当前在生产中的版本？ 当前为 Beta 版本，但在使用者将其投入生产时，它可能处于生产环境中的版本？ 不只是使用微服务解决的困难问题。

许多项目都依赖于这些库。 通过将微服务划分为每个存储库中的一个，可以通过使用内部存储库 Azure Artifacts 来最大程度地解决内部依赖关系。 库的生成会将其最新版本推送到 Azure Artifacts 以供内部使用。 还必须手动更新下游项目，才能依赖于新更新的包。

当在服务之间移动代码时，另一个缺点会自我呈现。 尽管将应用程序的第一个部分划分为100% 是微服务的，但实际上很少如此 prescient，因为这样做不会产生任何服务划分错误。 因此，功能和用于驱动它的代码将需要从服务迁移到服务：存储库。 当 leaping 从一个存储库到另一个存储库时，代码就会丢失其历史记录。 在许多情况下，尤其是在出现审核事件的情况下，对一段代码具有完整历史记录是非常有用的。

最后和可能最重要的缺点是协调更改。 在真正的微服务应用程序中，服务之间不应有部署依赖关系。 可以按任何顺序部署服务 A、B 和 C，因为这些服务具有松耦合。 但实际上，在某些情况下，需要同时进行跨多个存储库的更改。 一些示例包括更新库以关闭安全漏洞或更改所有服务使用的通信协议。

若要进行跨存储库更改，需要对每个存储库进行提交。 每个存储库中的每个更改都需要请求并单独查看。 这种情况很难协调，通常会令人讨厌。

使用多个存储库的另一种方法是将所有源代码放在一个非常简单的、所有已知的单个存储库中。

### <a name="single-repository"></a>单个存储库

在此方法中，有时称为[monorepository](https://danluu.com/monorepo/)，每个服务的所有源代码都置于相同的存储库中。 最初，这看起来很可能会使源代码处理变得难以处理。 但有些标记的优点是以这种方式工作。

第一个优点是更易于管理项目之间的依赖关系。 项目可以直接导入另一个项目源，而不是依赖于某个外部的项目源。 这意味着在开发人员工作站上的编译时，可能会发现更新是即时的，并且可能会发现冲突的版本。 实际上，改变了一些集成测试的左侧部分。

在项目间移动代码时，现在可以更轻松地保留历史记录，因为文件将被检测为已移动而不是重新编写。

另一个优点是，跨越服务边界的各种更改都可以在单个提交中进行。 这可以减少可能会对多个更改进行单独检查的开销。

许多工具都可以对代码执行静态分析，以检测不安全的编程做法或 Api 的问题使用。 在多存储库世界中，需要循环访问每个存储库，以找出其中的问题。 单个存储库允许在一个位置运行分析。

单个存储库方法也有很多缺点。 最担心的一点是，只有单个存储库引发了安全问题。 如果存储库中每个服务模型的内容泄漏，则丢失的代码量最小。 使用单个存储库，公司拥有的一切都可能会丢失。 在过去的这种情况下，有很多示例，将整个游戏开发工作。 如果有多个存储库公开了较少的外围应用，这是大多数安全做法中非常需要的特征。

单个存储库的大小可能无法快速进行管理。 这会带来一些有趣的性能影响。 可能需要使用专用的工具（例如[用于 Git 的虚拟文件系统](https://vfsforgit.org/)），这种方法最初旨在改进 Windows 团队开发人员的体验。

通常，使用单个存储库的参数会归结为 Facebook 或 Google 使用此方法进行源代码排列的参数。 如果这种方法对于这些公司来说是足够的，当然，这是适用于所有公司的正确方法。 这种情况的一个事实是，很少有公司对 Facebook 或 Google 的规模等内容进行操作。 在这些规模上出现的问题与大多数开发人员将面临的问题不同。 对于看，goose 的好处可能并不好。

最终，可以使用解决方案来托管微服务的源代码。 但在大多数情况下，在单个存储库中运行的管理和工程开销不值得 meager。 将代码拆分在多个存储库上有助于更好地分离关注点并鼓励开发团队之间自治。  

### <a name="standard-directory-structure"></a>标准目录结构

不管是单个还是多个存储库，每个服务都将有自己的目录。 若要使开发人员可以快速地在项目之间进行交互，最佳优化之一就是维护一种标准目录结构。

![图11-3 电子邮件和登录服务的标准目录结构](./media/dir-struct.png)

每当创建新项目时，都应使用放置正确结构的模板。 此模板还可以将此类有用项包含为框架 README 文件和 `azure-pipelines.yml`。 在任何微服务的体系结构中，项目之间的差异很高，使得服务的大容量操作更困难。

有许多工具可为整个目录提供模板化，其中包含多个源代码目录。 [Yeoman](https://yeoman.io/)在 JavaScript 领域中很受欢迎，GitHub 最近发布了[存储库模板](https://github.blog/2019-06-06-generate-new-repositories-with-repository-templates/)，它们提供了很多相同的功能。

## <a name="task-management"></a>任务管理

在任何项目中管理任务都很困难。 最前面的问题是为了确保开发人员的工作效率，要解决的有关工作流的排序问题。

云本机应用程序通常比传统软件产品更小，或至少将其划分为较小的服务。 跟踪与这些服务相关的问题或任务与任何其他软件项目一样重要。 无人希望失去对某些工作项的跟踪，或者向客户说明未正确记录其问题。 板在项目级别配置，但在每个项目中都可以定义区域。 它们允许跨多个组件打破问题。 将整个应用程序的所有工作保存在一个位置的优点是，在更好地理解工作项时，可以轻松地将工作项从一个团队移动到另一个团队。

Azure DevOps 附带了一些预配置的热门模板。 在最基本的配置中，需要知道的是积压工作（backlog）、用户正在处理的内容以及执行的操作。 请务必了解构建软件的过程，以便将工作转换为客户的优先级并完成任务。 当然，很少有软件项目只是 `to do`、`doing`和 `done`这一过程。 人们开始向进程添加 `QA` 或 `Detailed Specification` 等步骤并不需要花费很长时间。

敏捷方法的一个更重要的部分是按固定的时间间隔自我自检。 这些检查旨在帮助用户了解团队面临的问题以及如何改进。 通常，这意味着通过开发过程更改问题和功能的流动。 因此，最好是通过其他阶段展开板的布局。

板中的阶段并不是唯一的组织工具。 根据板的配置，存在工作项的层次结构。 看板上可以显示的最精细的项是一项任务。 现在，任务包含标题的字段、说明、优先级、剩余工作量的估计值以及链接到其他工作项或开发项（分支、提交、拉取请求、生成等）的功能。 工作项可归入应用程序的不同区域和不同迭代（冲刺（sprint）），使其更易于查找。

![图 11-4 Azure DevOps 中的示例任务](./media/task-details.png)

"说明" 字段支持所需的常规样式（粗体、斜体下划线和删除线）以及插入图像的功能。 这使它成为一个非常强大的工具，可在指定工作或 bug 时使用。

任务可以汇总到功能中，这些功能定义了更大的工作单元。 功能又可以[汇总到长篇故事](https://docs.microsoft.com/azure/devops/boards/backlogs/define-features-epics?view=azure-devops)中。 利用此层次结构中的任务，可以更轻松地了解如何关闭大型功能。

![图11-5 基本过程模板中默认配置的工作项类型](./media/board-issue-types.png)

Azure Boards 中的问题有不同种类的视图。 尚未计划的项会出现在积压工作（backlog）中。 可以从此处将其分配给冲刺（sprint）。 冲刺（sprint）是一个时间段，在该时间段内，需要完成一些工作。 此工作可以包括任务，还可以包括票证的解析。 在此之后，可以从冲刺（Sprint）板部分管理整个冲刺（sprint）。 此视图显示了工作的进展情况，并提供了一个刻录图，以在冲刺（sprint）将成功时提供更新的估计值。

![图11-6 定义了冲刺（sprint）的板](./media/sprint-board.png)

到现在为止，Azure DevOps 中的主板有很大的强大功能。 对于开发人员来说，有很简单的视图可用于处理。 供项目经理查看即将到来的工作以及现有工作的概述。 对于管理人员，有许多关于管理和容量的报告。 遗憾的是，没有神奇的无需跟踪工作的云本机应用程序。 但如果您必须跟踪工作，则在某些情况下，体验比 Azure DevOps 更好。

## <a name="cicd-pipelines"></a>CI/CD 管道

除了持续集成（CI）和持续交付（CD）出现，软件开发生命周期中几乎没有任何变化。 更改后，将立即针对项目的源代码生成并运行自动测试，并提前捕获错误。 在持续集成生成的出现之前，从存储库中拉取代码并发现它未通过测试或甚至无法生成。 这会导致大量跟踪破损的源。

传统上，在生产环境中交付软件需要大量文档和步骤列表。 需要手动完成的每个步骤都需要在一个非常容易出错的过程中完成。

![图11-7 清单](./media/checklist.png)

持续集成的备用是持续交付，其中，将在环境中部署全新的生成包。 手动过程无法进行缩放以匹配开发速度，因此自动化变得更加重要。 清单由可以更快、更准确地执行相同任务的脚本替换。

持续交付交付的环境可能是一个测试环境，也可能是由许多主要技术公司来完成的，它可能是生产环境。 后者要求对高质量的测试投资，这会使更改不会对用户产生中断。 与持续集成在代码早期持续交付中发现问题的方式相同，这是及早捕获部署过程中的问题。

自动执行生成和传递过程的重要性由云本机应用程序突出。 部署发生的频率更高，更多，因此无法在不可能的情况上手动部署边框。

### <a name="azure-builds"></a>Azure 版本

Azure DevOps 提供了一套工具，使持续集成和部署比以往更容易。 这些工具位于 Azure Pipelines 下。 第一个是 Azure 版本，它是一种用于在规模上运行基于 YAML 的生成定义的工具。 用户可以使用自己的生成计算机（在生成需要精心设置环境时非常有用），也可以从不断刷新的 Azure 托管虚拟机池使用计算机。 这些托管生成代理随各种开发工具预安装，不仅适用于 .NET 开发，而且还适用于从 Java 到 Python 到 iPhone 开发的所有内容。

DevOps 包括范围广泛的现成生成定义，可针对任何生成进行自定义。 生成定义在名为 `azure-pipelines.yml` 的文件中定义，并签入到存储库中，以便它们可以与源代码一起进行版本控制。 这样就可以更轻松地在分支中对生成管道进行更改，因为可以将更改签入到该分支。 图11-8 显示了在完整框架上构建 ASP.NET web 应用程序的示例 `azure-pipelines.yml`。

```yml
name: $(rev:r)

variables:
  version: 9.2.0.$(Build.BuildNumber)
  solution: Portals.sln
  artifactName: drop
  buildPlatform: any cpu
  buildConfiguration: release
  
pool:
  name: Hosted VS2017
  demands:
  - msbuild
  - visualstudio
  - vstest

steps:
- task: NuGetToolInstaller@0
  displayName: 'Use NuGet 4.4.1'
  inputs:
    versionSpec: 4.4.1

- task: NuGetCommand@2
  displayName: 'NuGet restore'
  inputs:
    restoreSolution: '$(solution)'

- task: VSBuild@1
  displayName: 'Build solution'
  inputs:
    solution: '$(solution)'
    msbuildArgs: '-p:DeployOnBuild=true -p:WebPublishMethod=Package -p:PackageAsSingleFile=true -p:SkipInvalidConfigurations=true -p:PackageLocation="$(build.artifactstagingdirectory)\\"'
    platform: '$(buildPlatform)'
    configuration: '$(buildConfiguration)'

- task: VSTest@2
  displayName: 'Test Assemblies'
  inputs:
    testAssemblyVer2: |
     **\$(buildConfiguration)\**\*test*.dll
     !**\obj\**
     !**\*testadapter.dll
    platform: '$(buildPlatform)'
    configuration: '$(buildConfiguration)'

- task: CopyFiles@2
  displayName: 'Copy UI Test Files to: $(build.artifactstagingdirectory)'
  inputs:
    SourceFolder: UITests
    TargetFolder: '$(build.artifactstagingdirectory)/uitests'

- task: PublishBuildArtifacts@1
  displayName: 'Publish Artifact'
  inputs:
    PathtoPublish: '$(build.artifactstagingdirectory)'
    ArtifactName: '$(artifactName)'
  condition: succeededOrFailed()
```

**图 11-8** -示例 azure-pipelines. docker-compose.override.yml

此生成定义使用许多内置任务，使创建生成的操作与构建设置（比巨大的 Millennium Falcon 简单）简单。 例如，NuGet 任务还原 NuGet 包，而 VSBuild 任务调用 Visual Studio 生成工具来执行实际编译。 Azure DevOps 中有数百个不同的任务，社区维护了数千个不同的任务。 您可能不知道您想要运行哪些生成任务，而有人已经生成了一个任务。

可以通过签入、计划或完成其他生成来手动触发生成。 在大多数情况下，需要对每个签入进行构建。 可以对生成进行筛选，以使不同的生成针对存储库的不同部分或不同的分支运行。 这可以实现这样的方案：运行快速生成，减少对拉取请求的测试，并在夜间针对中继运行完整的回归分析套件。

生成的最终结果是一组称为 "生成项目" 的文件。 这些项目可传递到生成过程中的下一步或添加到 Azure 项目源，以便其他生成使用。

### <a name="azure-devops-releases"></a>Azure DevOps 版本

构建负责将软件编译到可交付的包中，但仍需要将项目推送到测试环境以完成持续交付。 为此，Azure DevOps 使用名为 release 的单独工具。 版本使用的是可用于生成的相同任务库，但引入了 "阶段" 的概念。 阶段是安装包的隔离环境。 例如，产品可能使用开发、QA 和生产环境。 代码持续交付到可在其中运行自动测试的开发环境。 一旦这些测试通过，版本就会移到 QA 环境进行手动测试。 最后，将代码推送到生产环境中，其中的每个人都可以看到该代码。

![图11-9 使用开发、QA 和生产阶段的示例发布管道](./media/release-pipeline.png)

生成中的每个阶段都可以在上一阶段完成后自动触发。 但在许多情况下，这并不是理想的做法。 将代码移动到生产中可能需要对他人的批准。 版本通过允许审批者在发布管道的每个步骤中实现此操作。 可以设置规则，以便特定人员或人员组在发布到生产环境之前，必须在发布上注销。 这些入口允许进行手动质量检查，还可满足任何与控制生产环境相关的法规要求。

### <a name="everybody-gets-a-build-pipeline"></a>每个人获取生成管道

配置多个生成管道并无开销，因此，每个微服务至少有一个生成管道。 理想情况下，微服务可独立部署到任何环境，因此，每个环境都可以通过自己的管道释放，而不会产生大量无关的代码。 每个管道都可以有自己的一组审批，使每个服务的生成过程变体变体。

### <a name="versioning-releases"></a>版本控制

使用发布功能的一个缺点是它无法在签入的 `azure-pipelines.yml` 文件中定义。 出于许多原因，你可能想要执行此操作，因为有多个分支版本定义可将发布主干添加到项目模板中。 幸运的是，工作正在努力将部分支持转移到生成组件。 这会被称为多阶段生成，而[第一版现在可用](https://devblogs.microsoft.com/devops/whats-new-with-azure-pipelines/)！

>[!div class="step-by-step"]
>[上一页](azure-security.md)
>[下一页](infrastructure-as-code.md)