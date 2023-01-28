# Probability-Calculator

### Scientific Computing with Python, course offered by freecodecamp.org

This is an experiment that calculates probability of drawing whatever color and count of balls you choose from a hat. 

Instructions for building this project can be found at https://www.freecodecamp.org/learn/scientific-computing-with-python/scientific-computing-with-python-projects/probability-calculator


        import random
        import copy

        class Hat:

            def __init__(self, **ball_type):
                self.ball_type = ball_type
                self.contents = []
                for k, v in self.ball_type.items():
                    self.contents += [k]*v

            def draw(self, draws):    
                if draws > len(self.contents):
                    return self.contents
                balls_drawn = random.choices(self.contents, k=draws)
                for ball in balls_drawn:
                    self.contents.remove(ball)
                return balls_drawn

        def experiment(hat, expected_balls, 
                    num_balls_drawn, 
                    num_experiments):

            successful_experiments = 0
            for i in range(num_experiments):
                new_hat = copy.deepcopy(hat)
                balls_drawn = new_hat.draw(num_balls_drawn)
                if all(balls_drawn.count(ball) >= expected_balls[ball] for ball in expected_balls):
                    successful_experiments += 1
            probability = successful_experiments / num_experiments
            return probability

