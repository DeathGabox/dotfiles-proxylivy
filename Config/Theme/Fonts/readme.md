```
wget https://github.com/ryanoasis/nerd-fonts/releases/download/v2.3.3/Hack.zip
unzip Hack.zip
mkdir /usr/share/fonts/Hack
mv Hack\ Regular\ Nerd\ Font\ Complete.ttf /usr/share/fonts/Hack/
mv Hack\ Regular\ Nerd\ Font\ Complete\ Mono.ttf /usr/share/fonts/Hack/
rm *.ttf Hack.zip LICENSE.md readme.md
wget https://github.com/ryanoasis/nerd-fonts/releases/download/v2.3.3/JetBrainsMono.zip
unzip JetBrainsMono.zip
mkdir /usr/share/fonts/JetBrains
mv JetBrains\ Mono\ Regular\ Nerd\ Font\ Complete.ttf /usr/share/fonts/JetBrains/
mv JetBrains\ Mono\ Regular\ Nerd\ Font\ Complete\ Mono.ttf /usr/share/fonts/JetBrains/
rm *.ttf JetBrainsMono.zip readme.md OFL.txt
fc-cache
