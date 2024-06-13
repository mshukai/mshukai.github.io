<div id="article_content" class="article_content clearfix">
        <link rel="stylesheet" href="https://csdnimg.cn/release/blogv2/dist/mdeditor/css/editerView/kdoc_html_views-1a98987dfd.css">
        <link rel="stylesheet" href="https://csdnimg.cn/release/blogv2/dist/mdeditor/css/editerView/ck_htmledit_views-044f2cf1dc.css">
                <div id="content_views" class="markdown_views prism-atom-one-dark">
                    <svg xmlns="http://www.w3.org/2000/svg" style="display: none;">
                        <path stroke-linecap="round" d="M5,0 0,2.5 5,5z" id="raphael-marker-block" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);"></path>
                    </svg>
                    <p>使用<a href="https://so.csdn.net/so/search?q=ESLint&amp;spm=1001.2101.3001.7020" target="_blank" class="hl hl-1" data-report-click="{&quot;spm&quot;:&quot;1001.2101.3001.7020&quot;,&quot;dest&quot;:&quot;https://so.csdn.net/so/search?q=ESLint&amp;spm=1001.2101.3001.7020&quot;,&quot;extra&quot;:&quot;{\&quot;searchword\&quot;:\&quot;ESLint\&quot;}&quot;}" data-tit="ESLint" data-pretit="eslint">ESLint</a>很久了，也看了ESLint官方文档很多遍，但对于ESLint配置的规则还是不胜清楚，例如：</p> 
<pre data-index="0" class="set-code-show prettyprint"><code class="prism language-javascript has-numbering" onclick="mdcp.copyCode(event)" style="position: unset;"><span class="token punctuation">{<!-- --></span>
  <span class="token string">"extends"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span><span class="token string">"plugin:prettier/recommended"</span><span class="token punctuation">]</span>
<span class="token punctuation">}</span>
<div class="hljs-button {2}" data-title="复制"></div></code><ul class="pre-numbering" style=""><li style="color: rgb(153, 153, 153);">1</li><li style="color: rgb(153, 153, 153);">2</li><li style="color: rgb(153, 153, 153);">3</li></ul></pre> 
<p>上面extends的值为什么要"plugin:"开头？这里的prettier插件需要显示安装吗？像这样<code>plugins: ["prettier"]</code>。</p> 
<pre data-index="1" class="set-code-show prettyprint"><code class="prism language-javascript has-numbering" onclick="mdcp.copyCode(event)" style="position: unset;"><span class="token punctuation">{<!-- --></span>
  <span class="token string">"plugins"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span><span class="token string">"prettier"</span><span class="token punctuation">]</span><span class="token punctuation">,</span>
  <span class="token string">"rules"</span><span class="token punctuation">:</span> <span class="token punctuation">{<!-- --></span>
    <span class="token string">"prettier/prettier"</span><span class="token punctuation">:</span> <span class="token string">"error"</span>
  <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
<div class="hljs-button {2}" data-title="复制"></div></code><ul class="pre-numbering" style=""><li style="color: rgb(153, 153, 153);">1</li><li style="color: rgb(153, 153, 153);">2</li><li style="color: rgb(153, 153, 153);">3</li><li style="color: rgb(153, 153, 153);">4</li><li style="color: rgb(153, 153, 153);">5</li><li style="color: rgb(153, 153, 153);">6</li></ul></pre> 
<p>上面规则<code>"prettier/prettier": "error"</code>表示的是插件prettier中的规则prettier吧？</p> 
<pre data-index="2" class="set-code-show prettyprint"><code class="prism language-javascript has-numbering" onclick="mdcp.copyCode(event)" style="position: unset;"><span class="token punctuation">{<!-- --></span>
  <span class="token string">"extends"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span><span class="token string">"prettier"</span><span class="token punctuation">]</span><span class="token punctuation">,</span>
<span class="token punctuation">}</span>
<div class="hljs-button {2}" data-title="复制"></div></code><ul class="pre-numbering" style=""><li style="color: rgb(153, 153, 153);">1</li><li style="color: rgb(153, 153, 153);">2</li><li style="color: rgb(153, 153, 153);">3</li></ul></pre> 
<p>上面的规则extends值为啥又没有<code>"plugin:"</code>前缀了呢？</p> 
<p>为了解释上面的几个问题，首先要从ESLint的插件和共享配置说起。</p> 
<h3><a name="t0"></a><a id="ESLint_27"></a>ESLint插件</h3> 
<p>ESLint的规则十分便于扩展，而扩展的途径就是为ESLint添加插件，插件文件的基础格式是：<br> 我们创建一个插件叫<code>eslint-plugin-myplugin</code></p> 
<pre data-index="3" class="prettyprint set-code-show"><code class="prism language-javascript has-numbering" onclick="mdcp.copyCode(event)" style="position: unset;">module<span class="token punctuation">.</span>exports <span class="token operator">=</span> <span class="token punctuation">{<!-- --></span>
	configs<span class="token punctuation">:</span> <span class="token punctuation">{<!-- --></span>
      config1<span class="token punctuation">:</span> <span class="token punctuation">{<!-- --></span>
        plugins<span class="token punctuation">:</span> <span class="token punctuation">[</span><span class="token string">'myplugin'</span><span class="token punctuation">]</span><span class="token punctuation">,</span>
        rules<span class="token punctuation">:</span> <span class="token punctuation">{<!-- --></span>
			<span class="token string">"myplugin/rule1"</span><span class="token punctuation">:</span> <span class="token string">"error"</span>
		<span class="token punctuation">}</span>
	  <span class="token punctuation">}</span>
    <span class="token punctuation">}</span><span class="token punctuation">,</span>
	rules<span class="token punctuation">:</span> <span class="token punctuation">{<!-- --></span>
	  rule1<span class="token punctuation">:</span> <span class="token punctuation">{<!-- --></span>
	    create<span class="token punctuation">:</span> <span class="token keyword">function</span> <span class="token punctuation">(</span>context<span class="token punctuation">)</span> <span class="token punctuation">{<!-- --></span>
	        <span class="token comment">// rule implementation ...</span>
	    <span class="token punctuation">}</span>
	  <span class="token punctuation">}</span>
	<span class="token punctuation">}</span>
<span class="token punctuation">}</span>
<div class="hljs-button {2}" data-title="复制"></div></code><ul class="pre-numbering" style=""><li style="color: rgb(153, 153, 153);">1</li><li style="color: rgb(153, 153, 153);">2</li><li style="color: rgb(153, 153, 153);">3</li><li style="color: rgb(153, 153, 153);">4</li><li style="color: rgb(153, 153, 153);">5</li><li style="color: rgb(153, 153, 153);">6</li><li style="color: rgb(153, 153, 153);">7</li><li style="color: rgb(153, 153, 153);">8</li><li style="color: rgb(153, 153, 153);">9</li><li style="color: rgb(153, 153, 153);">10</li><li style="color: rgb(153, 153, 153);">11</li><li style="color: rgb(153, 153, 153);">12</li><li style="color: rgb(153, 153, 153);">13</li><li style="color: rgb(153, 153, 153);">14</li><li style="color: rgb(153, 153, 153);">15</li><li style="color: rgb(153, 153, 153);">16</li><li style="color: rgb(153, 153, 153);">17</li></ul></pre> 
<p>上面编写的ESLint插件包含了两部分，一个是rules部分定义了这个插件自定义的规则，这里对应的是规则<code>rule1</code>。另一个是配置部分configs字段定义的规则集合，这里对应了<code>config1</code>。</p> 
<h3><a name="t1"></a><a id="myplugin_51"></a>使用插件myplugin</h3> 
<p>在插件中引入的规则和配置可以在项目的ESLint配置文件中使用。<br> 插件中定义的规则（插件中rules下定义的规则）使用方法如下：</p> 
<pre data-index="4" class="set-code-show prettyprint"><code class="prism language-javascript has-numbering" onclick="mdcp.copyCode(event)" style="position: unset;"><span class="token punctuation">{<!-- --></span>
	<span class="token string">"plugins"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span><span class="token string">"myplugin"</span><span class="token punctuation">]</span><span class="token punctuation">,</span> <span class="token comment">// 可以将eslint-plugin这个前缀省略</span>
	<span class="token string">"rules"</span><span class="token punctuation">:</span> <span class="token punctuation">{<!-- --></span>
		<span class="token string">"myplugin/rule1"</span><span class="token punctuation">:</span> <span class="token string">"error"</span>
	<span class="token punctuation">}</span>
<span class="token punctuation">}</span>
<div class="hljs-button {2}" data-title="复制"></div></code><ul class="pre-numbering" style=""><li style="color: rgb(153, 153, 153);">1</li><li style="color: rgb(153, 153, 153);">2</li><li style="color: rgb(153, 153, 153);">3</li><li style="color: rgb(153, 153, 153);">4</li><li style="color: rgb(153, 153, 153);">5</li><li style="color: rgb(153, 153, 153);">6</li></ul></pre> 
<p>在配置文件中使用插件中的规则首先需要安装插件（在plugins下引入插件），然后才能在rules字段下加上插件名 + / + ruleName的形式使用插件中定义的规则。</p> 
<p>除了使用插件中定义的规则，还可以使用插件中定义好的配置（confings字段下定义的内容）。<br> 使用插件中的配置则不需要像使用插件中的规则一样显示安装插件（plugins: […]）。</p> 
<pre data-index="5" class="set-code-show prettyprint"><code class="prism language-javascript has-numbering" onclick="mdcp.copyCode(event)" style="position: unset;"><span class="token punctuation">{<!-- --></span>
	<span class="token string">"extends"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span><span class="token string">"plugin:myplugin/config1"</span><span class="token punctuation">]</span>
<span class="token punctuation">}</span>
<div class="hljs-button {2}" data-title="复制"></div></code><ul class="pre-numbering" style=""><li style="color: rgb(153, 153, 153);">1</li><li style="color: rgb(153, 153, 153);">2</li><li style="color: rgb(153, 153, 153);">3</li></ul></pre> 
<p>在extends字段中使用 plugin:pluginName/configName 的形式使用插件中定义的指定配置。<br> 为什么需要plugin作为前缀了呢？<br> 因为extends继承的配置有两个来源，一个是插件中定义的，就像上面介绍的，eslint-config-configname也可以生成可共享配置。</p> 
<h3><a name="t2"></a><a id="eslintconfigmyconfig_74"></a>eslint-config-myconfig</h3> 
<p>定义一个用于共享的配置包，这个包的名字最好以eslint-config开头。</p> 
<pre data-index="6" class="set-code-show prettyprint"><code class="prism language-javascript has-numbering" onclick="mdcp.copyCode(event)" style="position: unset;">module<span class="token punctuation">.</span>exports <span class="token operator">=</span> <span class="token punctuation">{<!-- --></span>
	rules<span class="token punctuation">:</span> <span class="token punctuation">{<!-- --></span>
		<span class="token operator">...</span>
	<span class="token punctuation">}</span>
<span class="token punctuation">}</span>
<div class="hljs-button {2}" data-title="复制"></div></code><ul class="pre-numbering" style=""><li style="color: rgb(153, 153, 153);">1</li><li style="color: rgb(153, 153, 153);">2</li><li style="color: rgb(153, 153, 153);">3</li><li style="color: rgb(153, 153, 153);">4</li><li style="color: rgb(153, 153, 153);">5</li></ul></pre> 
<p>定义好的包，可以在ESLint的配置文件中使用。</p> 
<pre data-index="7" class="set-code-show prettyprint"><code class="prism language-javascript has-numbering" onclick="mdcp.copyCode(event)" style="position: unset;"><span class="token punctuation">{<!-- --></span>
	<span class="token string">"extends"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span><span class="token string">"myconfig"</span><span class="token punctuation">]</span>
<span class="token punctuation">}</span>
<div class="hljs-button {2}" data-title="复制"></div></code><ul class="pre-numbering" style=""><li style="color: rgb(153, 153, 153);">1</li><li style="color: rgb(153, 153, 153);">2</li><li style="color: rgb(153, 153, 153);">3</li></ul></pre> 
<p>直接 <code>extends: [configName]</code> 就完成了对配置文件的继承。</p> 
<h2><a name="t3"></a><a id="_91"></a>参考</h2> 
<p><a href="https://github.com/prettier/eslint-config-prettier/blob/main/index.js">eslint-config-prettier</a><br> <a href="https://github.com/prettier/eslint-plugin-prettier/blob/master/eslint-plugin-prettier.js">eslint-plugin-prettier</a></p>
                </div><div><div></div></div>
                <link href="https://csdnimg.cn/release/blogv2/dist/mdeditor/css/editerView/markdown_views-f23dff6052.css" rel="stylesheet">
                <link href="https://csdnimg.cn/release/blogv2/dist/mdeditor/css/style-c216769e99.css" rel="stylesheet">
        </div>