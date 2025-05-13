# Projektkurs-inom-programvaruutveckling

En simulering av passningsspel i fotboll samt tränarens optimala position på planen.

## 🔧 URL

https://hemming1983.github.io/Fotboll/

## 🔧 Tutorial

Guide: Porting a C/SDL Program to WebAssembly Using Emscripten

1. Prerequisites
- A working SDL2 program written in C
- SDL_image and SDL_ttf if using images or text
- Windows/macOS/Linux
- Git and Python (for running a local test server)
- Emscripten SDK
  
2. Install Emscripten SDK
git clone https://github.com/emscripten-core/emsdk.git
cd emsdk
./emsdk install latest
./emsdk activate latest
./emsdk_env.ps1 (for PowerShell)
Verify installation with: emcc --version

3. Install Python (if you don't already have it)
- Download from https://www.python.org/downloads/
- Check "Add Python to PATH" during installation
- Test with: python --version
  
4. Modify your code
- Add: #include <emscripten/emscripten.h>
- Create functions: void update(...), void render(...)
- Replace the game loop with: emscripten_set_main_loop(...);
  
5. Folder Structure
/Project
|-- source/ (C source and headers)
|-- resources/ (images and fonts)
|-- index.html (entry point)

7. Compile to WebAssembly
emcc source/main.c source/GameController.c source/GameModel.c source/GameView.c ^
-o index.html ^
-s USE_SDL=2 ^
-s USE_SDL_IMAGE=2 ^
-s SDL2_IMAGE_FORMATS='["png"]' ^
-s USE_SDL_TTF=2 ^
--preload-file resources

9. Test Locally
python -m http.server
Then open in a browser: http://localhost:8000

11. Deploy to GitHub Pages
git init
git add .
git commit -m "Initial WebAssembly version"
git remote add origin https://github.com/YOURNAME/YOURREPO.git
git push -u origin main
Go to GitHub -> Settings -> Pages -> Choose branch 'main' and folder '/ (root)'
Your URL will be: https://YOURNAME.github.io/YOURREPO/

13. .gitignore example
*.o
*.tmp
*.log
*.wasm
*.js
*.html
emsdk/
emscripten_cache/
.DS_Store
