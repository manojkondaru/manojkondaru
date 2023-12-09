#include <SDL.h>

SDL_Window* window;
SDL_Renderer* renderer;
SDL_Texture* dinoTexture;
SDL_Rect dinoRect;

void init() {
    SDL_Init(SDL_INIT_VIDEO);
    window = SDL_CreateWindow("Dino Run", SDL_WINDOWPOS_UNDEFINED, SDL_WINDOWPOS_UNDEFINED, 800, 600, 0);
    renderer = SDL_CreateRenderer(window, -1, SDL_RENDERER_ACCELERATED);
    
    // Load Dino image
    SDL_Surface* dinoSurface = SDL_LoadBMP("dino.bmp");
    dinoTexture = SDL_CreateTextureFromSurface(renderer, dinoSurface);
    SDL_FreeSurface(dinoSurface);

    // Set initial position of the Dino
    dinoRect.x = 100;
    dinoRect.y = 400;
    dinoRect.w = 50;
    dinoRect.h = 50;
}

void handleInput() {
    SDL_Event event;
    while (SDL_PollEvent(&event)) {
        if (event.type == SDL_QUIT) {
            SDL_Quit();
            exit(0);
        }
        if (event.type == SDL_KEYDOWN) {
            if (event.key.keysym.sym == SDLK_SPACE) {
                // Jump logic here
            }
        }
    }
}

void update() {
    // Update game logic here
}

void render() {
    SDL_RenderClear(renderer);
    SDL_RenderCopy(renderer, dinoTexture, NULL, &dinoRect);
    SDL_RenderPresent(renderer);
}

int main() {
    init();

    while (1) {
        handleInput();
        update();
        render();
        SDL_Delay(16); // Cap the frame rate
    }

    return 0;
}
