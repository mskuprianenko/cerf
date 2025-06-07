endogenous_growth.py

class EndogenousGrowthModel:
    def __init__(self, A,  α  , K, L, £, ®, β):
        self.A = A   Уровень технологий
        self. α   =  α     Коэффициент эластичности по капиталу
        self.K = K   Начальный капитал
        self.L = L   Начальный труд
        self.£= £ Норма сбережений
        self.®= ® Норма амортизации
        self.β = β   Коэффициент влияния на технологии
        self.time = 0   Время
        self.history = []   История значений для визуализации

    def production(self):
        »Вычисление валового выпуска на текущий момент времени.»
        return self.A  (self.K  self. α  )  (self.L  (1 - self. α  ))

    def technological_change(self, investment):
        »Изменение уровня технологий по результатам инвестиций.»
        self.A += self.beta  investment

    def capital_accumulation(self):
        »Динамика накопления капитала.»
        investment = self.savings_rate  self.production()
        self.K += investment - (self.depreciation_rate  self.K)   Накопление капитала

         Сохраняем данные для визуализации
        self.history.append({
            'time': self.time,
            'A': self.A,
            'K': self.K,
            'Y': self.production(),
            'investment': investment
        })

    def simulate_growth(self, years):
        »Симуляция роста на заданное количество лет.»
        for _ in range(years):
            self.time += 1
            self.capital_accumulation()
            investment = self.savings_rate  self.production()
            self.technological_change(investment)

    def get_history(self):
        »Получение истории значений для анализа и визуализации.»
        return self.history

 Пример использования класса
if __name__ == "__main__":
    model = EndogenousGrowthModel(
        A=1.0,            Начальный уровень технологий
         α  =0.3,        Распределение капитала
        K=1000,           Начальный капитал
        L=500,            Начальный уровень труда
        savings_rate=0.2,   Норма сбережений
        depreciation_rate=0.05,   Норма амортизации капитала
        beta=0.1          Влияние инвестиций на технологии
    )
    model.simulate_growth(50)   Симуляция роста на 50 лет
    history = model.get_history()   Получение истории

