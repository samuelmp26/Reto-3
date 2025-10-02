if __name__ == "__main__":
    class Point:
        def __init__(self, x=0, y=0):
            self.x = x
            self.y = y
        def move(self, new_x, new_y):
            self.x = new_x
            self.y = new_y
        def reset(self):
            self.x = 0
            self.y = 0
        def compute_distance(self, point: "Point")-> float:
            distance = ((self.x - point.x)**2+(self.y - point.y)**2)**0.5
            return distance

    class Line:
        def __init__(self, start: Point, end: Point):
            self.start = start
            self.end = end
            self.length = self.compute_length()
            self.slope = self.compute_slope()
        def compute_length(self):
            return self.start.compute_distance(self.end)
        def compute_slope(self):
            dx = self.end.x - self.start.x
            dy = self.end.y - self.start.y
            if dx == 0:
                return 90.0
            return (dy/dx) * 57.2958   # aproximación de atan(dy/dx) en grados
        def compute_horizontal_cross(self):
            return (self.start.y <= 0 <= self.end.y) or (self.end.y <= 0 <= self.start.y)
        def compute_vertical_cross(self):
            return (self.start.x <= 0 <= self.end.x) or (self.end.x <= 0 <= self.start.x)
        def discretize_line(self, n):
            points = []
            for i in range(n+1):
                t = i/n
                x = self.start.x + t * (self.end.x - self.start.x)
                y = self.start.y + t * (self.end.y - self.start.y)
                points.append(Point(x, y))
            self.discrete_points = points
            return points

    class Rectangle:
        def __init__(self, **kwargs):
            if "bottom_left" in kwargs and "width" in kwargs and "height" in kwargs:
                bottom_left = kwargs["bottom_left"]
                width = kwargs["width"]
                height = kwargs["height"]
                self.width = width
                self.height = height
                self.center_point = Point(bottom_left.x + width/2, bottom_left.y + height/2)

            elif "center" in kwargs and "width" in kwargs and "height" in kwargs:
                center = kwargs["center"]
                self.width = kwargs["width"]
                self.height = kwargs["height"]
                self.center_point = center

            elif "corner1" in kwargs and "corner2" in kwargs:
                corner1 = kwargs["corner1"]
                corner2 = kwargs["corner2"]
                self.width = corner2.x - corner1.x
                self.height = corner2.y - corner1.y
                self.center_point = Point(corner1.x + self.width/2, corner1.y + self.height/2)

            elif "lines" in kwargs and len(kwargs["lines"]) == 4:
                lines = kwargs["lines"]
                xs = [line.start.x for line in lines] + [line.end.x for line in lines]
                ys = [line.start.y for line in lines] + [line.end.y for line in lines]
                self.width = max(xs) - min(xs)
                self.height = max(ys) - min(ys)
                self.center_point = Point((max(xs)+min(xs))/2, (max(ys)+min(ys))/2)

            else:
                raise ValueError("Argumentos inválidos para inicializar el rectángulo")

        def compute_area(self):
            return self.width * self.height
        def compute_perimeter(self):
            return 2 * (self.width + self.height)
        def compute_interference_point(self, point):
            left_limit_x = self.center_point.x - self.width / 2
            right_limit_x = self.center_point.x + self.width / 2    
            bottom_limit_y = self.center_point.y - self.height / 2
            top_limit_y = self.center_point.y + self.height / 2
            if left_limit_x <= point.x <= right_limit_x and bottom_limit_y <= point.y <= top_limit_y:
                return True
            else:
                return False
        def compute_interference_line(self, point1, point2):    
            left_limit_x = self.center_point.x - self.width / 2
            right_limit_x = self.center_point.x + self.width / 2    
            bottom_limit_y = self.center_point.y - self.height / 2
            top_limit_y = self.center_point.y + self.height / 2

            if self.compute_interference_point(point1) or self.compute_interference_point(point2):
                return True

            if min(point1.x, point2.x) <= right_limit_x and max(point1.x, point2.x) >= left_limit_x \
                and min(point1.y, point2.y) <= top_limit_y and max(point1.y, point2.y) >= bottom_limit_y:
                    return True

            return False

    class Square(Rectangle):    
        def __init__(self, side, center_point):
            super().__init__(center=center_point, width=side, height=side)

    # Ejemplo que use para probar
    point1 = Point(1, 2)
    point2 = Point(7, 3)
    rect1 = Rectangle(corner1=point1, corner2=point2)
    print("Área:", rect1.compute_area())
    print("Perímetro:", rect1.compute_perimeter())
    print("Punto de interferencia (3,2):", rect1.compute_interference_point(Point(3, 2)))


    # Otra prueba con líneas
    l1 = Line(Point(1,1), Point(5,1))
    l2 = Line(Point(5,1), Point(5,4))
    l3 = Line(Point(5,4), Point(1,4))
    l4 = Line(Point(1,4), Point(1,1))
    rect2 = Rectangle(lines=[l1,l2,l3,l4])
    print("Área rectángulo con líneas:", rect2.compute_area())
