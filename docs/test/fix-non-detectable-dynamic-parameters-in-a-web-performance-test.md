---
title: 修复 Visual Studio 的 Web 性能测试中无法检测的动态参数 | Microsoft Docs
ms.date: 10/19/2016
ms.topic: article
helpviewer_keywords:
- walkthroughs, load tests
- load tests, walkthroughs
- load tests, correlating dynamic parameters
ms.assetid: 92dff25c-36ee-4135-acdd-315c4962fa11
author: gewarren
ms.author: gewarren
manager: ghogen
ms.technology: vs-ide-test
ms.openlocfilehash: dc92b65ba26b11fe65919fd94ac16c8480427f6b
ms.sourcegitcommit: 900ed1e299cd5bba56249cef8f5cf3981b10cb1c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/19/2018
---
# <a name="fix-non-detectable-dynamic-parameters-in-a-web-performance-test"></a>在 Web 性能测试中修复无法检测的动态参数

有些网站使用动态参数来处理某些 Web 请求。 动态参数是指其值在用户每次运行应用程序时重新生成的参数。 动态参数的一个示例就是会话 ID。 会话 ID 通常每隔 5 到 30 分钟就会发生更改。 Web 性能测试记录器和播放引擎可自动处理最常见的动态参数类型：

-   在 Cookie 值中设置的动态参数值。 Web 性能测试引擎会在播放时自动处理这些参数值。

-   在 HTML 页的隐藏字段中设置的动态参数值，如 ASP.NET 视图状态。 这些参数值可由记录器自动处理，这将向测试添加隐藏字段提取规则。

-   设置为查询字符串或窗体发布参数的动态参数值。 这些参数值将在记录 Web 性能测试后通过动态参数检测进行处理。

未检测到某些类型的动态参数。 未检测到的动态参数将在你运行 Web 性能测试时导致失败，因为每次运行测试时的动态值都有所不同。 若要正确处理这些参数，可以在 Web 性能测试中手动向动态参数添加提取规则。

## <a name="create-and-run-a-web-app-with-dynamic-parameters"></a>创建和运行带动态参数的 Web 应用程序

为了演示可检测的和无法检测的动态参数，我们将创建一个简单的 ASP.NET Web 应用程序，该应用程序具有带几个控件和一些自定义代码的三个 Web 窗体。 我们接下来将了解如何隔离和处理动态参数。

1.  创建一个名为 DynamicParamaterSample 的新 ASP.NET 项目。

     ![创建空的 ASP.NET Web 应用程序项目](../test/media/web_test_dynamicparameter_aspproject.png "Web_Test_DynamicParameter_ASPProject")

2.  添加名为 Querystring.aspx 的 Web 窗体。

3.  在设计视图中，将 HiddenField 拖动到页面上，然后将 (ID) 属性的值更改为 HiddenFieldSessionID。

     ![添加 HiddenField](../test/media/web_test_dynamicparameter_hiddenfield.png "Web_Test_DynamicParameter_HiddenField")

4.  更改为 Querystring 页的源视图，并添加以下用于生成模拟会话 ID 动态参数的突出显示的 ASP.NET 和 JavaScript 代码：

    ```html
    <head runat="server">
    <title>JavaScript dynamic property correlation sample</title><script type="text/javascript" language="javascript">    <!--        function jScriptQueryString()         {            var Hidden = document.getElementById("HiddenFieldSessionID");            var sessionId = Hidden.value;            window.location = 'JScriptQuery.aspx?CustomQueryString=jScriptQueryString___' + sessionId;         }    //--></script>
    </head>
    <body>
        <form id="form1" runat="server">
        <div>
             <a name="QuerystringHyperlink" href="ASPQuery.aspx?CustomQueryString=ASPQueryString___<%= Session.SessionID %>">Dynamic querystring generated by ASP.net</a>         <br/>         <br/>         <a href="javascript:jScriptQueryString()">Dynamic querystring generated by javascript </a>
        </div>
        <asp:HiddenField ID="HiddenFieldSessionID" runat="server" />
        </form>
    </body>
    </html>
    ```

5.  打开 Querystring.aspx.cs 文件，并将以下突出显示的代码添加到 Page_Load 方法：

    ```csharp
    public partial class Querystring : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
            Session.Add("Key", "Value");HiddenFieldSessionID.Value = Session.SessionID;
        }
    }
    ```

6.  添加另一个名为 ASPQuery.aspx 的 Web 窗体。

7.  在设计视图中，将标签拖动到页面上，并将其 (ID) 属性的值更改为 IndexLabel。

     ![向 Web 表单添加标签](../test/media/web_test_dynamicparameter_label.png "Web_Test_DynamicParameter_Label")

8.  将超链接拖动到页面上，并将其 Text 属性的值改为“Back”。

     ![添加指向 Web 表单的超链接](../test/media/web_test_dynamicparameter_hyperlink.png "Web_Test_DynamicParameter_Hyperlink")

9. 为 NavigationURL 属性选择 (…)。

     ![编辑 NavigateURL 属性](../test/media/web_test_dynamicparameter_hyperlink_navurl.png "Web_Test_DynamicParameter_Hyperlink_NavURL")

     选择 Querystring.aspx。

     ![选择 URL 为 Querystring.aspx](../test/media/web_test_dynamicparameter_hyperlink_navurl2.png "Web_Test_DynamicParameter_Hyperlink_NavURL2")

10. 打开 ASPQuery.aspx.cs 文件，并将以下突出显示的代码添加到 Page_Load 方法：

    ```csharp
    protected void Page_Load(object sender, EventArgs e)
            {
                int index;            string qstring;            string dateportion;            string sessionidportion;            qstring = Request.QueryString["CustomQueryString"];            index = qstring.IndexOf("___");            dateportion = qstring.Substring(0, index);            index += 3;            sessionidportion = qstring.Substring(index, qstring.Length - index);            if (sessionidportion != Session.SessionID)            {                Response.StatusCode = 401;                IndexLabel.Text = "Failure!  Invalid querystring parameter found.";            }            else            {                IndexLabel.Text = "Success.  Dynamic querystring parameter was found.";            }            IndexLabel.Text += "<br>\r\n";
            }
    ```

11. 添加第三个名为 JScriptQuery.aspx 的 Web 窗体。

     正如我们在第二页上进行的操作，将标签拖动到窗体上，将其 (ID) 属性设置为 IndexLabel 并将超链接拖动到窗体上，将其文本属性设置为“Back”并将其 NavigationURL 属性设置为 Querystring.aspx。

     ![添加和配置第三个 Web 表单](../test/media/web_test_dynamicparameter_addwebform3.png "Web_Test_DynamicParameter_AddWebForm3")

12. 打开 JScriptQuery.aspx.cs 文件，并将以下突出显示的代码添加到 Page_Load 方法：

    ```csharp
    protected void Page_Load(object sender, EventArgs e)
            {
                int index;            string qstring;            string dateportion;            string sessionidportion;            qstring = Request.QueryString["CustomQueryString"];            index = qstring.IndexOf("___");            dateportion = qstring.Substring(0, index);            index += 3;            sessionidportion = qstring.Substring(index, qstring.Length - index);            if (sessionidportion != Session.SessionID)            {                Response.StatusCode = 401;                IndexLabel.Text = "Failure!  Invalid querystring parameter found.";            }            else            {                IndexLabel.Text = "Success.  Dynamic querystring parameter was found.";            }            IndexLabel.Text += "<br>\r\n";
            }
    ```

13. 保存项目。

14. 在解决方案资源管理器中，将 Querystring.aspx 设置为起始页。

     ![在 Querystring.aspx 上设置起始页](../test/media/web_test_dynamicparameter_setstartpage.png "Web_Test_DynamicParameter_SetStartPage")

15. 按 Ctrl+F5 在浏览器中运行该 Web 应用程序。 复制 URL。 当记录你的测试时，你将需要它。

16. 尝试这两个链接。 它们都会显示消息“Success. Dynamic querystring parameter found.”（成功。已找到动态查询字符串参数。）

     ![运行 Web 应用](../test/media/web_test_dynamicparameter_runapp.png "Web_Test_DynamicParameter_RunApp")

     ![成功！](../test/media/web_test_dynamicparameter_runapp2.png "Web_Test_DynamicParameter_RunApp2")

## <a name="create-a-web-performance-test"></a>创建 Web 性能测试

1.  将 Web 性能和负载测试项目添加到你的解决方案。

     ![添加 Web 性能测试和负载测试项目](../test/media/web_test_dynamicparameter_addtestproject.png "Web_Test_DynamicParameter_AddTestProject")

2.  将 WebTest1.webtest 重命名为 DynamicParameterSampleApp.webtest。

     ![重命名 Web 性能测试](../test/media/web_test_dynamicparameter_renametest.png "Web_Test_DynamicParameter_RenameTest")

3.  记录测试。

     ![记录 Web 性能测试](../test/media/web_test_dynamicparameter_recordtest.png "Web_Test_DynamicParameter_RecordTest")

4.  将你正在测试的网站中的 URL 复制并粘贴到浏览器中。

     ![粘贴正在测试的网站的 URL](../test/media/web_test_dynamicparameter_recordtest2.png "Web_Test_DynamicParameter_RecordTest2")

5.  浏览 Web 应用程序。 依次选择 ASP.NET 链接、“后退”链接、javascript 链接（后跟返回链接）。

     Web 测试记录器可在你浏览 Web 应用程序时显示 HTTP 请求和响应 URL。

6.  在测试记录器上选择“停止”按钮。

     用于检测动态参数的对话框显示了一个进度栏，该进度栏显示了接收到的 HTTP 响应中的参数检测状态。

7.  将自动检测 ASPQuery 页中的 CustomQueryString 的动态参数。 但是，不会检测 JScriptQuery 页中的 CustomQueryString 的动态参数。

     选择“确定”以向 Querystring.aspx 添加提取规则，并将其绑定到 ASPQuery 页。

     ![提升未检测到的动态参数](../test/media/web_test_dynamicparameter_promotedialog.png "Web_Test_DynamicParameter_PromoteDialog")

     提取规则将添加到 Querystring.aspx 的第一个请求。

     ![已向请求添加提取规则](../test/media/web_test_dynamicparameter_autoextractionrule.png "Web_Test_DynamicParameter_AutoExtractionRule")

     在 ASPQuery.aspx 的请求树中展开第二个请求，你会看到 CustomQueryString 的值已绑定到该提取规则。

     ![CustomQueryString 绑定到提取规则](../test/media/web_test_dynamicparameter_autoextractionrule2.png "Web_Test_DynamicParameter_AutoExtractionRule2")

8.  保存测试。

## <a name="run-the-test-to-isolate-the-non-detected-dynamic-parameter"></a>运行测试以隔离无法检测的动态参数

1.  运行测试。

     ![运行该 Web 性能测试](../test/media/web_test_dynamicparameter_runtest.png "Web_Test_DynamicParameter_RunTest")

2.  JScriptQuery.aspx 页的第四个请求失败。 转到 Web 测试。

     ![测试结果中的动态参数错误](../test/media/web_test_dynamicparameter_runresults.png "Web_Test_DynamicParameter_RunResults")

     JScriptQuery.aspx 请求节点突出显示在编辑器中。 展开节点，您会发现 CustomQueryString 的“1v0yhyiyr0raa2w4j4pwf5zl”部分似乎是动态的。

     ![CustomQueryString 中的可疑动态参数](../test/media/web_test_dynamicparameter_runresults2.png "Web_Test_DynamicParameter_RunResults2")

3.  返回到 Web 性能测试结果查看器，然后选择失败的 JScriptQuery.aspx 页。 然后，选择请求选项卡并验证是否清除“显示原始数据”复选框，向下滚动并选择“在 CustomQueryString 上快速查找”。

     ![使用快速查找隔离该动态参数](../test/media/web_test_dynamicparameter_runresultsquckfind.png "Web_Test_DynamicParameter_RunResultsQuckFind")

4.  从测试编辑器中可以看到，已为 JScriptQuery.aspx 请求的 CustomQueryString 分配值：`jScriptQueryString___1v0yhyiyr0raa2w4j4pwf5zl`，并且怀疑的动态部分为“1v0yhyiyr0raa2w4j4pwf5zl”。 在“查找内容”下拉列表中，移除该搜索字符串的可疑部分。 该字符串应为“CustomQueryString=jScriptQueryString___”。

     动态参数将存在错误的请求前面的一个请求中进行赋值。 因此，请选中“向上搜索”复选框，然后选择“查找下一个”，直到 Querystring.aspx 前面的请求突出显示在“请求”面板中。 此情况应在您选择“查找下一个”三次后发生。

     ![使用快速查找隔离该动态参数](../test/media/web_test_dynamicparameter_runresultsquckfind4.png)

     正如“响应”选项卡和以下显示的之前实现的 JavaScript 所示，向查询字符串参数 CustomQueryString 分配值“jScriptQueryString___”，并且该字符串参数还会与变量 sessionId 的返回值串联。

    ```
    function jScriptQueryString()          {             var Hidden = document.getElementById("HiddenFieldSessionID");             var sessionId = Hidden.value;             window.location = 'JScriptQuery.aspx?CustomQueryString=jScriptQueryString___' + sessionId;          }

    ```

     现在我们已了解发生错误的位置且需要提取 sessionId 的值。 但是，提取值是纯文本，因此我们需要通过尝试找到显示 sessionId 的实际值的字符串来进一步隔离该错误。 通过查看代码，可以看到变量 sessionId 等于 HiddenFieldSessionID 所返回的值。

5.  使用 HiddenFieldSessionID 上的快速查找，清除“向上搜索”复选框并选择当前请求。

     ![在 HiddenFieldSession 上使用快速查找](../test/media/web_test_dynamicparameter_runresultsquckfindhiddensession.png "Web_Test_DynamicParameter_RunResultsQuckFindHiddenSession")

     你会看到，该返回值与原始 Web 性能测试记录中的返回值不是同一字符串。 对于此测试运行，返回的值为“5w4v3yrse4wa4axrafykqksq”，而在原始记录中，该值为“1v0yhyiyr0raa2w4j4pwf5zl”。 由于该值与原始记录不匹配，因此将会产生错误。

6.  由于我们必须修复原始记录的动态参数，因此请在工具栏上选择记录的结果。

     ![选择记录的结果](../test/media/web_test_dynamicparameter_recordedresult.png "Web_Test_DynamicParameter_RecordedResult")

7.  在记录的结果中，选择第三个请求，即你在测试运行结果中隔离的相同的 Querystringrequest.aspx 请求。

     ![在记录的结果中选择相同的请求](../test/media/web_test_dynamicparameter_recordedresultsselectnode.png "Web_Test_DynamicParameter_RecordedResultsSelectNode")

     选择“响应”选项卡，向下滚动并选择您之前隔离的原始动态参数值“1v0yhyiyr0raa2w4j4pwf5zl”，然后添加提取规则。

     ![为该动态参数添加提取规则](../test/media/web_test_dynamicparameter_recordedresultaddextractionrule.png "Web_Test_DynamicParameter_RecordedResultAddExtractionRule")

     新提取规则将添加到 Querystring.aspx 请求，并分配有值“Param0”。

     如果该对话框通知我们已找到要与参数绑定的提取文本的匹配项，请选择“是”。

     ![已创建提取规则](../test/media/web_test_dynamicparameter_addextractiondialog.png "Web_Test_DynamicParameter_AddExtractionDialog")

8.  选择“查找下一个”。 我们需要更改第一个匹配项，它是 JScriptQuery 页的 CustomQueryString 的参数。

     ![查找和替换参数的文本](../test/media/web_test_dynamicparameter_addextractionfindreplace.png "Web_Test_DynamicParameter_AddExtractionFindReplace")

9. 选择“替换”。

     ![用参数替换文本](../test/media/web_test_dynamicparameter_addextractionfindreplace2.png "Web_Test_DynamicParameter_AddExtractionFindReplace2")

     JScriptQuery.aspx 请求下的 QueryString 参数将使用新的上下文参数“CustomQueryString=jScriptQueryString___{{Param0}}”进行更新。

     ![应用于查询字符串的参数](../test/media/web_test_dynamicparameter_addextractionfindreplace3.png "Web_Test_DynamicParameter_AddExtractionFindReplace3")

10. 关闭“查找和替换”对话框。 请注意，检测到的动态参数与关联的未检测到的动态参数具有类似的请求树结构。

     ![检测到并已关联动态参数](../test/media/web_test_dynamicparameter_conclusion.png "Web_Test_DynamicParameter_Conclusion")

11. 运行测试。 它现在运行，而不会失败。

## <a name="qa"></a>问题解答

### <a name="q-can-i-re-run-dynamic-parameter-detection-if-my-web-app-gets-modified"></a>问：如果我的 Web 应用程序已被修改，我是否可以重新运行动态参数检测？

 答：可以，请使用下列过程：

1.  在工具栏中，选择“将动态参数提升为 Web 测试参数”按钮。

     完成检测过程之后，如果检测到任何动态参数，则将显示“将动态参数提升为 Web 测试参数”对话框。

     动态参数将在“动态参数”列下列出。 从中提取动态参数以及绑定到动态参数的请求将在“从响应中提取参数”和“绑定到请求”列下列出。

     如果在“将动态参数提升为 Web 测试参数”对话框中选择动态参数，则会在 Web 性能测试编辑器请求树中突出显示两个请求。 第一个请求是将添加提取规则的请求。 第二个请求是将绑定提取值的位置。

2.  选中或清除要自动关联的动态参数旁边的复选框。 默认情况下会选中所有动态参数。

### <a name="q-do-i-need-to-configure-visual-studio-to-detect-dynamic-parameters"></a>问：我是否需要将 Visual Studio 配置为检测动态参数？

 答：当记录 Web 性能测试时，默认的 Visual Studio 配置为检测动态参数。 但是，如果将 Visual Studio 选项配置为不检测动态参数，或使用其他动态参数修改了所测试的 Web 应用程序；仍可[从 Web 性能测试编辑器运行动态参数检测](#FindingNonDetectableDynamicParamters_QA_ReRunDetection)。