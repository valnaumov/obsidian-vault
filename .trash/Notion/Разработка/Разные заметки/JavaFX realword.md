# Conduktor

Был пост на Апворке.

[Add our desktop software to macOS brew + CI/CD - Upwork](https://www.upwork.com/jobs/Add-our-desktop-software-macOS-brew_%7E01ffd8a6d02e330ea4?source=rss)

from

[JavaFX](https://www.upwork.com/ab/feed/jobs/rss?api_params=1&orgUid=601068921942224897&paging=0%3B10&q=javafx&securityToken=3303988d994d03194b418c13663220993d33461f5d89e6f95759312eb3d403b9b2a9d1b312e64d27cf7ac42600869ece17a9cccde52ae1f720029791fcf7995a&sort=recency&userUid=601068921933836288)

Mon Jun 28 2021 13:32:55 (1 hour)

# 1.

Context:  
We want to be added to brew cask (cask because we are not open-source)  
for our macOS users to easily install our application. You must already  
have done it.  
  
Our application:  
  
Conduktor Desktop is a JavaFX application (embeds its own JVM runtime)  
which installs in /Applications/Conduktor.app. Our CI/CD builds a .pkg.  
We want this to be &quot;brew-able&quot; now.  
  
Our scripts:  
  
- Our releases are publicly available at  
github.com/conduktor/builds/releases and - Our CI/CD here:  
github.com/conduktor/builds/blob/master/.github/workflows/build.yml\#L195-L209  
  
Your task:  
  
- Create a new formula at brew's  
  
- In our CI/CD (linked above), add usage of `brew bump-formula-pr` to automatically create an update PR in brew's repo.  
**Budget**: $100  
  
**Posted On**: June 28, 2021 05:32 UTC**Category**: DevOps Engineering**Skills**:CI/CD Pipelines, Automation Software Release, Application Installer, Desktop Applications, macOS

  

Т.е. есть смысл попробовать залить на brew. Когда буду делать Sample App, где откатаю новую джаву и проч. Хотя это не первостепенное, первый раз такое вижу.