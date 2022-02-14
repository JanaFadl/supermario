#include <iostream>

#include <SFML/Graphics.hpp>
#include <SFML/Audio.hpp>
#include <SFML/System.hpp>
#include <SFML/Window.hpp>
#include <SFML/Network.hpp>
#include "Animation.h"
using namespace std;
using namespace sf;

int main()
{
    
    bool canjump = true;
    Clock animation_clock;
    Clock coin_clock;

    RenderWindow window(VideoMode(1500, 400), "SuperMario");

    RectangleShape layer(Vector2f(750.0,390.0));
    layer.setPosition(0, 0);
    Texture sky;
    sky.loadFromFile("skyy.png");
    layer.setTexture(&sky);

    RectangleShape layer2(Vector2f(1500.0, 390.0));
    layer2.setPosition(740, 0);
    Texture sky2;
    sky2.loadFromFile("skyy.png");
    layer2.setTexture(&sky2);

    RectangleShape shape(Vector2f(75.0f, 75.0f));
    shape.setPosition(70, 0);
    Texture mario;
    mario.loadFromFile("mario4.PNG");
    shape.setTexture(&mario);
    shape.setScale(0.7, 1);
    shape.setTextureRect(IntRect(0, 0, 16, 32));
    int animationIndicator = 0;

    RectangleShape ground(Vector2f(75.0f, 75.0f));
    ground.setPosition(0, 375);
    Texture Ground;
    Ground.loadFromFile("ground.png");
    ground.setTexture(&Ground);
    ground.setScale(13,0.7);
    //ground.setTextureRect(IntRect(0, 0, 16, 32));
    //ground.setPosition(ground.getGlobalBounds().width, 400 - ground.getGlobalBounds().height);
    RectangleShape groundd(Vector2f(75.0f, 75.0f));
    groundd.setPosition(1000, 375);
    Texture Groundd;
    Groundd.loadFromFile("ground.png");
    groundd.setTexture(&Groundd);
    groundd.setScale( 10, 0.7);

        Font font;
        font.loadFromFile("./BackToSchoolPersonalUseRegular-w1xX2.ttf");
        Text text;
        text.setFont(font);
        text.setString("S c o r e = ");
        text.setFillColor(Color(0,0,0));
        text.setPosition(10, 10);
        text.setCharacterSize(35);
        text.setStyle(Text::Underlined);

        SoundBuffer buffer;
        buffer.loadFromFile("overworld.ogg");
        Sound sound;
        sound.setBuffer(buffer);
        sound.play();
        //bool sound getLoop();
    
        

        Texture coinTexture;
        coinTexture.loadFromFile("coins.png");
        Sprite coin(coinTexture);
        coin.setPosition(500, 300);
        coin.setTextureRect(sf::IntRect(0, 0, 36, 32));
        int coin_animation_indicator = 0;
        bool isCoinVisable = true;

        //if (isCoinVisable = false) {
        //    SoundBuffer buffer;
        //    buffer.loadFromFile("coin.ogg");
        //    Sound sound;
        //    sound.setBuffer(buffer);
        //    sound.play();
        //}

    while (window.isOpen())
    {
        Event event;
        while (window.pollEvent(event))
        {

            if (event.type == Event::Closed) {

                cout << "End";
                window.close();

            }
            Time time;
            float start = 0;
        }

        if (event.type == Event::KeyPressed); {
        }
        if (Keyboard::isKeyPressed(Keyboard::D)) {

            shape.move(Vector2f(0.2, 0.0));
            if (animation_clock.getElapsedTime().asSeconds() > 0.3) {
                animationIndicator++;
                animation_clock.restart();
            }
            shape.setScale(0.7, 1);

        }
        if (Keyboard::isKeyPressed(Keyboard::A)) {
            shape.move(Vector2f(-0.2, 0.0));
            if (animation_clock.getElapsedTime().asSeconds() > 0.3) {
                animationIndicator++;
                animation_clock.restart();
            }
            shape.setScale(-0.7, 1);
        }
        animationIndicator = animationIndicator % 3;
       shape.setTextureRect(sf::IntRect(animationIndicator * 16, 0, 16, 32));

       if (shape.getGlobalBounds().intersects(coin.getGlobalBounds())) {
           isCoinVisable = false;
       }
        if (Keyboard::isKeyPressed(Keyboard::Key::Space)&& canjump) {
            shape.move(Vector2f(0.0, -100.0));
            canjump = false;
        }
        if (!shape.getGlobalBounds().intersects(ground.getGlobalBounds())) {
            shape.move(Vector2f(0, 0.00001));
        }
       // if (!shape.getGlobalBounds().intersects(groundd.getGlobalBounds())) {
       //     shape.move(Vector2f(0, 0.00001));
       // }
        else {
            canjump = true;
        }
        if (coin_clock.getElapsedTime().asSeconds() > 0.2) {
            coin_animation_indicator++;
            coin_clock.restart();

            coin.setTextureRect(sf::IntRect(coin_animation_indicator * 36, 0, 36, 32));
            coin_animation_indicator++;
            coin_animation_indicator = coin_animation_indicator % 6;
        }

        for (int i = 0; i < 100; i++) 
        {
            if (!shape.getGlobalBounds().intersects(ground.getGlobalBounds()))
            {
                shape.move(0, 0.001);
            }


        }
        
      animationIndicator = animationIndicator % 3;
        shape.setTextureRect(IntRect(animationIndicator * 16, 0, 16, 32));

        window.clear();
        window.draw(layer);
        window.draw(layer2);

        window.draw(text);
        window.draw(ground);
        window.draw(groundd);
        if (isCoinVisable) window.draw(coin);
        
        window.draw(shape);
        window.display();
        //Time=clock
        //for(size_t i =0; ;i<=100000; i ++)

    }


    return 0;
}
