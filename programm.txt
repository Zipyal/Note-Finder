#include <iostream>
#include <string>

// Получение имени ноты
std::string getNoteName(int noteIndex) {
    const std::string notes[] = {"F", "E", "D", "C", "B", "A", "G"};
    return notes[noteIndex % 7];
}

// Вычисление октавы
int getOctave(int baseOctave, int offset) {
    return baseOctave + offset / 7;
}

// Определение ноты и октавы
std::pair<std::string, int> getNoteAndOctave(int linePosition) {
    int baseLine = 2; // Линия для ноты "G"
    int baseOctave = 1; // Октава для ноты "G"
    int offset = linePosition - baseLine;
    std::string note = getNoteName((7 + (offset % 7)) % 7);
    int octave = getOctave(baseOctave, offset);
    return {note, octave};
}

int main() {
    while (true) {
        int linePosition;

        // Ввод местоположения ноты от пользователя
        std::cout << "Введите местоположение ноты (линия: 2 для G1, 3 для A1, 4 для B1 и т.д., -1 для выхода): ";
        std::cin >> linePosition;

        // Условие выхода
        if (linePosition == -1) {
            std::cout << "Выход из программы." << std::endl;
            break;
        }

        // Проверка ввода
        if (linePosition < 0 || linePosition > 10) {
            std::cerr << "Ошибка: Введите позицию от 0 до 10." << std::endl;
            continue;
        }

        // Получение ноты и октавы
        auto [note, octave] = getNoteAndOctave(linePosition);

        // Вывод результата
        std::cout << "Нота: " << note << octave << std::endl;
    }

    return 0;
}