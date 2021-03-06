开发者注意事项
=================


分支和合并代码
--------------------
我们使用标准的git 体系结构，git存储库包含两个特殊分支：包含已发布的代码版本的主分支和包含未来版本中要包含的所有开发的开发分支。分支模型还为其他分支提供了三个类别：大多数开发发生的功能分支、用于准备新代码发布的发布分支和修补程序分支用于已发布的代码中的错误修复的修补程序这与旧的常见工作实践不同，在这种做法中，主和开发在同一个分支（主干）中，后者也是发布准备和修复错误的地方。

典型的开发将首先创建一个功能分支（名为 feature/great_new_stuff），在那里进行开发工作。在大多数情况下，此分支是从开发分支创建的。一旦开发和测试了该功能，新代码将合并回开发分支中。

在同时进行工作的同时，其他开发可能已合并到开发分支中。原则上，开发人员有责任首先将开发分支合并到功能分支中，然后解决冲突。如果冲突很容易解决，情况就是这样。如果冲突更加难以解决，这将与引入冲突变更的开发人员合作完成，或者作为最后的手段，由整个代码的看守人来完成。

为了尽早发现冲突并更容易解决，现代实践建议经常将功能分支合并到开发分支中，并随着工作的进展频繁地将开发分支合并到功能分支中。在长期脱节工作之后，一个接一个地解决几个小冲突要比几个独立的事态发展产生的大规模冲突更为有效。早期检测鼓励开发人员之间进行讨论，以便在合并变得太难之前计划未来代码更改的合并。

现代软件设计还将有助于减少开发和合并过程中的冲突（如下所述）。

在某些时候，有必要准备代码的发布。这个过程发生在特定的版本分支中。一旦发布准备就绪并进行了充分测试，它就会合并到主版和开发分支中并进行标记。通常，标签将包含版本号（例如，主要版本为 2.0，次要版本为 2.1）。然后，主分支包含新的官方发布，并在开发分支基于该版本的基础上继续开发工作。

尽管在测试过程中采取了各种谨慎措施，但在任何软件中总会有（希望很少）错误需要修复。当在发行版中检测到此错误时，将从 master 分支创建一个修补程序分支来实施和测试修复程序。一旦实施了令人满意的修复程序，错误修复分支将合并到主分支和开发分支中，并且版本号将递增（创建一个新标签，次要版本号增加，例如从 2.1.0 增加到 2.1.1）。为了可重复性，永远不应移动现有标签。

有关更多详细信息，请参阅 git flow 入门指南。


forking 和 clone 存储库
---------------------------

GitHub 和类似的工具允许克隆或分叉仓库。具有推送权限到官方仓库的开发人员使用克隆。在这种情况下，开发人员被要求遵循 git flow 方法。没有推送权限到官方仓库的开发人员使用分叉。在分支仓库中工作的开发人员可以自由使用自己选择的工作流程，但我们建议 git flow。

在统一的数据同化和预测系统的背景下，我们推荐使用分叉机制。

实际上，每个开发人员都将在自己的仓库分叉上工作，然后从该工作中克隆以编辑代码。每个开发者都可以自由推送自己的工作（建议经常推送）。当贡献准备好合并到中央存储库中时，开发人员会发出拉取请求。开发人员可以从彼此的存储库中提取分支机构，并就共同功能进行协作。如果分支是由具有足够权限的人在那里拉出的，他们也可以在中央存储库上共享分支。这应该用于需要多个开发人员之间进行交互的功能。

在统一数据同化和预测系统的协作环境中，分叉方法的一个优点是可以递归方式使用中。所有合作伙伴都应商定一个中央存储库。从那里，每个合作伙伴都可以创建一个分叉，最好是自动同步。然后，在每个合作伙伴组织中，每个开发人员都会将其组织的分叉作为他们的中央存储对于大型合作伙伴组织，甚至可以按团队、小组或部门增加另一个级别。

操作守则的一个常见问题是安全。在提议的模型中，运营用户可以拥有自己所需的存储库的分叉。为了编译代码，将在本地磁盘上创建该存储库的克隆。如果手动同步分叉和克隆，除非操作用户主动提取新的更改，否则任何事情都不会发生。即使自动同步，用户也可以添加自己的标签或使用特定的提交来防止意外更改。根据操作准则的要求，操作克隆可以位于防火墙内和备份磁盘上。GitHub 作为基于云的服务存在，但可以将其安装在组织自己的服务器（GitHub Enterprise）上，因此分叉本身也可以位于受保护的网络中。


代码审查
-----------

审查过程的作用是控制分支的内容，特别是存储库的开发分支和主分支。科学性质的讨论和决策应该在 ZenHub 级别进行，然后才能达到拉取请求 (PR) 和代码审查的水平。

什么是代码审查？
^^^^^^^^^^^^^^^^^^^^

**代码审查** 是对软件源代码的系统检查，旨在发现潜在的错误、检查逻辑并改善代码库运行状况。代码审查作为 **拉取请求 (PR)** 提交的一部分进行

谁来审查
^^^^^^^^^^^^^^^^^^^^^

功能更新的批准
>>>>>>>>>>>>>>>>>>>>>>>>>>
首先，所有的功能更新必须经过测试，其次，提交的更新必须经过数字签名

功能更新由如下成员中其中两人批准：(暂定)

    * 李健
    * 梁旭东
    * 武天杰


测试
--------


测试是开发过程的必要步骤，未经事先测试，不得合并任何分支。

为了帮助开发人员和审阅者履行职责，生态系统包括了测试代码的工具。开发测试、环境应该使添加和运行测试变得容易。

尽管各种系统存在一些测试，但是将测试添加到现有集合中应该被视为开发过程的一部分。开发人员是为其代码编写测试的最佳人选，所有主要开发都应该包括在其相关测试中。测试应与系统的任何其他部分一样进行审查，任何绕过或放宽测试标准的做法都应该有充分的理由和记录在案。

将使用自动测试系统（例如 Go CD、Travis）。可以将此系统配置为对某些操作自动运行测试套件。例如，每次推送仓库时，测试都可以自动运行。测试也可以在每天晚上或每周末自动运行，并且可以配置为在多个平台和多个编译器上运行。

运行完整的操作套件作为测试是非常昂贵的，对于防止错误进入系统来说也不是最有帮助。将开发并提供一系列测试，从单元测试、回归测试到低分辨率和高分辨率应用测试。某些测试将包括代码性能标准，以防止系统中计算成本的意外或未被注意的蔓延。测试中还将包含用于检查源代码是否符合一组定义的编码规范的脚本，以促进审查过程。

环境将被配置为自动运行测试，拉取请求将被禁用，直到预先确定的套件中的所有测试都不会失败。出于效率和成本原因，这不能包括所有级别的测试。其他更昂贵的测试将定期在开发分支上运行，并在发现问题时向开发人员报告。这可以确保尽早发现问题，从而促进和加快向主分支机构准备新版本。

尽管测试将在某些操作上或在预定的时间自动运行，但开发人员可以随时在其分支上手动运行测试。我们将鼓励他们定期这样做，以便尽早发现潜在的问题并尽早解决问题。

创建文档
-----------

为了编写指南和手册，我们使用的是 Python 软件包的 Sphinx。

我们创建了一个 GitHub 仓库来保存名为 Tianjie-Wu/MIDAS-Docs 的文档。请将文档放在此存储库中，并将文档的相应链接和文本放在顶级 index.html 文件中。


