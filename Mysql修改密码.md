---


---

<h2 id="mysql修改密码的几种方法">Mysql修改密码的几种方法</h2>
<p>Written with <a href="https://stackedit.io/">月光</a>.</p>
<blockquote>
<p>方法1： 用SET PASSWORD命令</p>
</blockquote>
<pre><code>mysql -u root 　　
mysql&gt; SET PASSWORD FOR 'root'@enter code here'localhost' = PASSWORD('newpass');
</code></pre>
<blockquote>
<p>方法2：用mysqladmin 　　<br>
<code>mysqladmin -u root password "newpass"</code> 　<br>
　如果root已经设置过密码，采用如下方法 　　<br>
<code>mysqladmin -u root password oldpass "newpass"</code><br>
方法3： 用UPDATE直接编辑user表</p>
</blockquote>
<pre><code>mysql -u root 　　
mysql&gt; use mysql; 　　
mysql&gt; UPDATE user SET Password = PASSWORD('newpass') WHERE user = 'root'; 　　
mysql&gt; FLUSH PRIVILEGES; 
</code></pre>
<blockquote>
<p>在丢失root密码的时候，可以这样</p>
</blockquote>
<pre><code>mysqld_safe --skip-grant-tables&amp;mysql -u root mysql 　　
mysql&gt; UPDATE user SET password=PASSWORD("new password") WHERE user='root'; 　　
enter code here
mysql&gt; FLUSH PRIVILEGES;
</code></pre>

