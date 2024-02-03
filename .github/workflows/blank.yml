import java.awt.*;
import java.awt.event.KeyEvent;
import java.awt.event.KeyListener;
import javax.swing.*;

public class SnakeGame extends JFrame implements KeyListener {

    private int gridSize = 20;
    private int snakeLength = 1;
    private int[] snakeX, snakeY;
    private int foodX, foodY;
    private boolean gameOver = false;

    public SnakeGame() {
        setTitle("Snake Game");
        setSize(gridSize * 20, gridSize * 20);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLocationRelativeTo(null);

        snakeX = new int[gridSize * gridSize];
        snakeY = new int[gridSize * gridSize];

        snakeX[0] = gridSize / 2;
        snakeY[0] = gridSize / 2;

        generateFood();

        addKeyListener(this);
        setFocusable(true);
        setFocusTraversalKeysEnabled(false);

        Timer timer = new Timer(150, e -> move());
        timer.start();
    }

    private void generateFood() {
        foodX = (int) (Math.random() * gridSize);
        foodY = (int) (Math.random() * gridSize);
    }

    private void move() {
        if (!gameOver) {
            for (int i = snakeLength; i > 0; i--) {
                snakeX[i] = snakeX[i - 1];
                snakeY[i] = snakeY[i - 1];
            }

            switch (direction) {
                case KeyEvent.VK_UP:
                    snakeY[0]--;
                    break;
                case KeyEvent.VK_DOWN:
                    snakeY[0]++;
                    break;
                case KeyEvent.VK_LEFT:
                    snakeX[0]--;
                    break;
                case KeyEvent.VK_RIGHT:
                    snakeX[0]++;
                    break;
            }

            if (snakeX[0] == foodX && snakeY[0] == foodY) {
                snakeLength++;
                generateFood();
            }

            for (int i = 1; i < snakeLength; i++) {
                if (snakeX[i] == snakeX[0] && snakeY[i] == snakeY[0]) {
                    gameOver = true;
                }
            }

            if (snakeX[0] < 0 || snakeX[0] >= gridSize || snakeY[0] < 0 || snakeY[0] >= gridSize) {
                gameOver = true;
            }

            repaint();
        }
    }

    @Override
    public void keyTyped(KeyEvent e) {
    }

    @Override
    public void keyPressed(KeyEvent e) {
        direction = e.getKeyCode();
    }

    @Override
    public void keyReleased(KeyEvent e) {
    }

    private int direction = KeyEvent.VK_RIGHT;

    @Override
    public void paint(Graphics g) {
        super.paint(g);
        if (!gameOver) {
            for (int i = 0; i < gridSize; i++) {
                for (int j = 0; j < gridSize; j++) {
                    if (i == snakeX[0] && j == snakeY[0]) {
                        g.setColor(Color.GREEN);
                        g.fillRect(i * 20, j * 20, 20, 20);
                    } else if (i == foodX && j == foodY) {
                        g.setColor(Color.RED);
                        g.fillRect(i * 20, j * 20, 20, 20);
                    } else {
                        g.setColor(Color.GRAY);
                        g.drawRect(i * 20, j * 20, 20, 20);
                    }
                }
            }
        } else {
            g.setColor(Color.RED);
            g.setFont(new Font("Arial", Font.BOLD, 30));
            g.drawString("Game Over!", gridSize * 4, gridSize * 10);
        }
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> new SnakeGame().setVisible(true));
    }
}
