source "https://rubygems.org"

# 'minimal-mistakes-jekyll' 테마를 직접 명시합니다.
gem "minimal-mistakes-jekyll"

# GitHub Pages 환경과 호환성을 맞추기 위한 Gem 모음입니다.
gem "github-pages", group: :jekyll_plugins

# Ruby 3.0 이상에서 Jekyll을 실행하기 위해 필요합니다.
gem "webrick", "~> 1.7"

# Windows 환경에서 실시간 미리보기 성능을 향상시킵니다.
gem "wdm", ">= 0.1.0", :install_if => Gem.win_platform?

# Jekyll 플러그인들을 관리하는 그룹입니다.
group :jekyll_plugins do
  gem "jekyll-feed"
  gem "jekyll-gist"
  gem "jekyll-include-cache"
  gem "jekyll-paginate"
  gem "jekyll-sitemap"
  gem "jekyll-admin"
  gem "jekyll-livereload"
end