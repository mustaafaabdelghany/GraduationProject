# GraduationProject
GraduationProject
java
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;

public class ShapeApplet extends JApplet {
    private String currentShape;
    private Color currentColor;
    private int currentThickness;
    private boolean isFilledShape;
    private boolean isEraserMode;
    private JPanel drawingPanel;
    
    public void init() {
        currentShape = "Line";
        currentColor = Color.BLACK;
        currentThickness = 1;
        isFilledShape = false;
        isEraserMode = false;
        
        // Create the shape buttons
        JButton lineButton = new JButton("Line");
        JButton rectangleButton = new JButton("Rectangle");
        JButton ovalButton = new JButton("Oval");
        
        // Create the color buttons
        JButton redButton = new JButton("Red");
        JButton greenButton = new JButton("Green");
        JButton blueButton = new JButton("Blue");
        
        // Create the eraser button
        JButton eraserButton = new JButton("Eraser");
        
        // Create the fill button
        JCheckBox fillCheckBox = new JCheckBox("Filled");
        
        // Create the thickness slider
        JSlider thicknessSlider = new JSlider(1, 10, 1);
        thicknessSlider.setMajorTickSpacing(1);
        thicknessSlider.setPaintTicks(true);
        thicknessSlider.setPaintLabels(true);
        
        // Create the drawing panel
        drawingPanel = new JPanel() {
            protected void paintComponent(Graphics g) {
                super.paintComponent(g);
                
                if (isEraserMode) {
                    g.setColor(Color.WHITE);
                    g.fillRect(0, 0, getWidth(), getHeight());
                }
                
                g.setColor(currentColor);
                Graphics2D g2d = (Graphics2D) g;
                g2d.setStroke(new BasicStroke(currentThickness));
                
                if (currentShape.equals("Line")) {
                    g.drawLine(20, 20, getWidth() - 20, getHeight() - 20);
                } else if (currentShape.equals("Rectangle")) {
                    if (isFilledShape) {
                        g.fillRect(20, 20, getWidth() - 40, getHeight() - 40);
                    } else {
                        g.drawRect(20, 20, getWidth() - 40, getHeight() - 40);
                    }
                } else if (currentShape.equals("Oval")) {
                    if (isFilledShape) {
                        g.fillOval(20, 20, getWidth() - 40, getHeight() - 40);
                    } else {
                        g.drawOval(20, 20, getWidth() - 40, getHeight() - 40);
                    }
                }
            }
        };
        
        // Set the layout of the applet
        setLayout(new BorderLayout());
        JPanel controlPanel = new JPanel();
        controlPanel.setLayout(new FlowLayout());
        
        // Add the shape buttons to the control panel
        controlPanel.add(lineButton);
        controlPanel.add(rectangleButton);
        controlPanel.add(ovalButton);
        
        // Add the color buttons to the control panel
        controlPanel.add(redButton);
        controlPanel.add(greenButton);
        controlPanel.add(blueButton);
        
        // Add the eraser button to the control panel
        controlPanel.add(eraserButton);
        
        // Add the fill checkbox to the control panel
        controlPanel.add(fillCheckBox);
        
        // Add the thickness slider to the control panel
        controlPanel.add(thicknessSlider);
        
        // Add the drawing panel to the applet
        add(drawingPanel, BorderLayout.CENTER);
        add(controlPanel, BorderLayout.SOUTH);
        
        // Add action listeners to the shape buttons
        lineButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                currentShape = "Line";
                drawingPanel.repaint();
            }
        });
        
        rectangleButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                currentShape = "Rectangle";
                drawingPanel.repaint();
            }
        });
        
        ovalButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                currentShape = "Oval";
                drawingPanel.repaint();
            }
        });
        
        // Add action listeners to the color buttons
        redButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                currentColor = Color.RED;
                drawingPanel.repaint();
            }
        });
        
        greenButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                currentColor = Color.GREEN;
                drawingPanel.repaint();
            }
        });
        
        blueButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                currentColor = Color.BLUE;
                drawingPanel.repaint();
            }
        });
        
        // Add action listener to the eraser button
        eraserButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                isEraserMode = !isEraserMode;
               drawingPanel.repaint();
            }
        });
        
        // Add item listener to the fill checkbox
        fillCheckBox.addItemListener(new ItemListener() {
            public void itemStateChanged(ItemEvent e) {
                isFilledShape = fillCheckBox.isSelected();
                drawingPanel.repaint();
            }
        });
        
        // Add change listener to the thickness slider
        thicknessSlider.addChangeListener(new ChangeListener() {
            public void stateChanged(ChangeEvent e) {
                currentThickness = thicknessSlider.getValue();
                drawingPanel.repaint();
            }
        });
    }
}
