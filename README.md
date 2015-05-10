# fixtitle.java
make some change about title
/*
 * To change this template, choose Tools | Templates
 * and open the template in the editor.
 */
package ravaranch;
 
import java.awt.BorderLayout;
import java.awt.Color;
import java.awt.Dimension;
import java.awt.GridLayout;
import java.awt.event.MouseAdapter;
import java.awt.event.MouseEvent;
import java.awt.event.MouseListener;
import java.util.Random;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JPanel;
import javax.swing.JScrollPane;
 
/**
 *
 * @author Piet
 */
public class RavaRanch {
   public static void main(String[] args) {
      new RavaRanch();
   }
    
   public RavaRanch() {
      final int MAX_TILES = 100;
      final int TILE_SIZE = 30;
       
      JPanel panel = new JPanel(new GridLayout(MAX_TILES, MAX_TILES));
       
      MouseAdapter m = new MouseAdapter() {
         @Override
         public void mousePressed(MouseEvent m) {
            CathyLabel label = (CathyLabel) m.getSource();
            System.out.format("mouse pressed: row %d, col %d%n", label.row, label.column);
         }
         @Override
         public void mouseReleased(MouseEvent m) {
            CathyLabel label = (CathyLabel) m.getSource();
            System.out.format("mouse released: row %d, col %d%n", label.row, label.column);
         }
         @Override
         public void mouseClicked(MouseEvent m) {
            CathyLabel label = (CathyLabel) m.getSource();
            System.out.format("mouse clicked: row %d, col %d%n", label.row, label.column);
         }
      };
       
      Random random = new Random();
      Dimension d = new Dimension(TILE_SIZE, TILE_SIZE);
       
      for (int row = 0; row < MAX_TILES; row++) {
         for (int col = 0; col < MAX_TILES; col++) {
            Color c = new Color(random.nextInt(256), random.nextInt(256), random.nextInt(256));
            panel.add(new CathyLabel(row, col, m, c, d));
         }
      }
       
      JScrollPane pane = new JScrollPane(panel);
//      pane.setPreferredSize(new Dimension(30 * TILE_SIZE, 30 * TILE_SIZE));
       
      JFrame frame = new JFrame("Cathy's game");
//      frame.getContentPane().setPreferredSize(new Dimension(20 * TILE_SIZE, 20 * TILE_SIZE));
      frame.getContentPane().add(pane, BorderLayout.CENTER);
      frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
      frame.pack();
      frame.setLocationRelativeTo(null);
      frame.setVisible(true);
   }
}
 
class CathyLabel extends JLabel {
   int row;
   int column;
   Color background;
    
   public CathyLabel(int r, int c, MouseListener m, Color b, Dimension d) {
      row = r;
      column = c;
      addMouseListener(m);
      this.setBackground(b);
      this.addMouseListener(m);
      this.setMinimumSize(d);
      this.setMaximumSize(d);
      this.setPreferredSize(d);
      this.setOpaque(true);
   }
}
