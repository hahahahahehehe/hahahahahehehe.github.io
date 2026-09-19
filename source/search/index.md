---
title: 站内搜索
date: 2026-09-19
layout: page
---

<style>
.search-input-box{
    width: 100%;
    padding: 10px 14px;
    font-size: 16px;
    border: 1px solid #ddd;
    border-radius: 4px;
    margin-bottom: 20px;
}
.search-item{
    padding: 12px 0;
    border-bottom: 1px solid #eee;
}
.search-empty{
    color: #999;
    text-align: center;
    padding: 40px 0;
}
.search-cat-tag{
    font-size:13px;
    color:#666;
}
</style>

<input class="search-input-box" id="searchInput" placeholder="输入分类/标题/标签搜索" />
<div id="searchResult"></div>

<script>
// ✅ 关键点：search.json永远放在站点根目录，直接 /search.json
let searchData = [];
fetch("/search.json")
  .then(res => {
    if (!res.ok) throw new Error("文件404");
    return res.json();
  })
  .then(data => {
    searchData = data;
    const input = document.getElementById("searchInput");
    input.addEventListener("input", searchFunc);
  })
  .catch(err => {
    document.getElementById("searchResult").innerHTML = "<div class='search-empty'>索引加载失败</div>";
    console.error("err", err);
  });

function searchFunc(){
  const keyword = document.getElementById("searchInput").value.trim().toLowerCase();
  const resultBox = document.getElementById("searchResult");
  if(!keyword){
    resultBox.innerHTML = "";
    return;
  }
  const matchList = searchData.filter(post=>{
    const title = post.title ? post.title.toLowerCase() : "";
    const cats = post.categories ? post.categories.join(" ").toLowerCase() : "";
    return title.includes(keyword) || cats.includes(keyword);
  });

  if(matchList.length === 0){
    resultBox.innerHTML = `<div class='search-empty'>未找到匹配「${keyword}」的文章</div>`;
    return;
  }

  let html = `<p>共找到 ${matchList.length} 篇匹配文章</p>`;
  matchList.forEach(item=>{
    const catStr = item.categories ? item.categories.join(" / ") : "default";
    // 文章链接：item.path本身是相对路径，前面加 /
    const fullUrl =  item.url;
    html += `
    <div class="search-item">
      <h3><a href="${fullUrl}">${item.title}</a></h3>
      <div class="search-cat-tag">分类：${catStr}</div>
    </div>
    `;
  });
  resultBox.innerHTML = html;
}
</script>