class SigaGame:
    def __init__(self):
        self.board = [['E' for _ in range(5)] for _ in range(5)]
        self.current_player = 'R'  # الأحمر يبدأ
        self.initialize_board()
        
    def initialize_board(self):
        # توزيع افتراضي للأحجار (12 لكل لاعب)
        for row in range(5):
            for col in range(5):
                if (row, col) == (2, 2):
                    continue
                if row < 2 or (row == 2 and col < 2):
                    self.board[row][col] = 'R'
                elif row > 2 or (row == 2 and col > 2):
                    self.board[row][col] = 'W'
        
    def print_board(self):
        print("\n  0 1 2 3 4")
        for i, row in enumerate(self.board):
            print(i, end=' ')
            for cell in row:
                print(cell if cell != 'E' else '.', end=' ')
            print()
            
    def is_valid_move(self, from_row, from_col, to_row, to_col):
        # التحقق من الحدود
        if not (0 <= from_row < 5 and 0 <= from_col < 5):
            return False
        if not (0 <= to_row < 5 and 0 <= to_col < 5):
            return False
            
        # التحقق من وجود حجر اللاعب في الموقع الأصلي
        if self.board[from_row][from_col] != self.current_player:
            return False
            
        # التحقق من أن الوجهة فارغة
        if self.board[to_row][to_col] != 'E':
            return False
            
        # حساب المسافة
        dx = to_col - from_col
        dy = to_row - from_row
        
        # الحركة العادية (خطوة واحدة)
        if abs(dx) + abs(dy) == 1:
            return True
            
        # القفز فوق الخصم
        if abs(dx) == 2 and dy == 0:
            jumped_col = (from_col + to_col) // 2
            if self.board[from_row][jumped_col] not in ['R', 'W']:
                return False
            return True
        if abs(dy) == 2 and dx == 0:
            jumped_row = (from_row + to_row) // 2
            if self.board[jumped_row][from_col] not in ['R', 'W']:
                return False
            return True
            
        return False
        
    def make_move(self, from_row, from_col, to_row, to_col):
        if self.is_valid_move(from_row, from_col, to_row, to_col):
            # إزالة حجر الخصم إذا كان هناك قفز
            dx = to_col - from_col
            dy = to_row - from_row
            if abs(dx) == 2 or abs(dy) == 2:
                jumped_row = from_row + dy//2
                jumped_col = from_col + dx//2
                self.board[jumped_row][jumped_col] = 'E'
                
            # نقل الحجر
            self.board[to_row][to_col] = self.current_player
            self.board[from_row][from_col] = 'E'
            
            # تبديل اللاعب
            self.current_player = 'W' if self.current_player == 'R' else 'R'
            return True
        return False
        
    def check_winner(self):
        red_count = sum(row.count('R') for row in self.board)
        white_count = sum(row.count('W') for row in self.board)
        if red_count == 0:
            return 'W'
        if white_count == 0:
            return 'R'
        return None

def play_game():
    game = SigaGame()
    while True:
        game.print_board()
        print(f"لاعب الدور الحالي: {'أحمر (R)' if game.current_player == 'R' else 'أبيض (W')}")
        from_row = int(input("ادخل رقم الصف الحالي: "))
        from_col = int(input("ادخل رقم العمود الحالي: "))
        to_row = int(input("ادخل رقم الصف الهدف: "))
        to_col = int(input("ادخل رقم العمود الهدف: "))
        
        if game.make_move(from_row, from_col, to_row, to_col):
            winner = game.check_winner()
            if winner:
                game.print_board()
                print(f"الفائز هو اللاعب {'أحمر (R)' if winner == 'R' else 'أبيض (W')}!")
                break
        else:
            print("حركة غير صالحة، حاول مرة أخرى!")

if __name__ == "__main__":
    play_game()
