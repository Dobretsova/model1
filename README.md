import math

def calculate_gsd_risk(alanine, asparagine, aspartic_acid, glycine, glutamine, glutamic_acid):
    z = 288.780 + (1.326 * alanine) - (235.461 * aspartic_acid) - (14.813 * asparagine) - (4.032 * glycine) + (41.517 * glutamine) + (72.569 * glutamic_acid)
    p = 1 / (1 + math.exp(-z)) * 100
    return p

def get_risk_level(p):
    if p <= 0.557:
        return "Высокий риск"
    else:
        return "Низкий риск"

def main():
    print("Калькулятор гестационного сахарного диабета")
    alanine = float(input("Введите концентрацию аланина: "))
    asparagine = float(input("Введите концентрацию аспаргина: "))
    aspartic_acid = float(input("Введите концентрацию аспаргиновой кислоты: "))
    glycine = float(input("Введите концентрацию глицина: "))
    glutamine = float(input("Введите концентрацию глутамина: "))
    glutamic_acid = float(input("Введите концентрацию глутаминовой кислоты: "))

    p = calculate_gsd_risk(alanine, asparagine, aspartic_acid, glycine, glutamine, glutamic_acid)
    risk_level = get_risk_level(p)

    print(f"Риск гестационного сахарного диабета: {risk_level} ({p:.2f}%)")

if __name__ == "__main__":
    main()
