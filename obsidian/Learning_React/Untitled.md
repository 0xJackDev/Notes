```
 <div

      style={{

        backgroundColor: "#f0f4f4",

        minHeight: "100vh",

        position: "relative",

        overflow: "hidden", // Prevents scrolling

      }}

    >

      {/* QR Code Component */}

      <div

        style={{

          position: "absolute",

          bottom: "-25px", // Pushes down slightly

          left: "-20px", // Pushes left slightly

          width: "90vw",

          maxWidth: "60vw", // Restrict width for desktop

          height: "90vh", // Height adjusts for content

          backgroundColor: "#ffffff",

          borderRadius: "30px",

          boxShadow: "0px 4px 4px rgba(0, 0, 0, 0.25)",

          padding: "20px",

          border: "1px solid black",

        }}

      >

        {/* Title */}

        <h1

          style={{

            color: "#3e54a3",

            fontSize: "48px",

            fontWeight: "500",

            margin: "0 auto",

            paddingTop: "80px",

            maxWidth: "90%",

            textAlign: "center",

            overflowWrap: "break-word",

          }}

        >

          QR Code Component

        </h1>

  

        {/* Paragraph */}

        <p

          style={{

            color: "#1c2022",

            fontSize: "20px",

            lineHeight: "1.6",

            opacity: "0.8",

            textAlign: "center", // Ensures text stays centered

            margin: "20px auto", // Centers text

            marginLeft:"30px"

          }}

        >

          This is a Figma design file for a Frontend Mentor challenge. Figma is

          a design tool professional teams use to collaborate on projects. Need

          help using Figma?{" "}

          <a

            href="#"

            style={{

              textDecoration: "underline",

              fontWeight: "700",

            }}

          >

            Read our Figma for developers article

          </a>

        </p>

  

        {/* Image */}

        <div

          style={{

            position: "relative", // Relative positioning for alignment

            width: "80%",

            border: "10px solid black",

            borderRadius: "10px",

            overflow: "hidden",

            margin: "0 auto",

            top: "120px",

          }}

        >

          {/* Responsive Image */}

          <Image

            src="/images/desktop-design.jpg"

            alt="QR Code Design"

            layout="responsive" // Ensures proper scaling

            width={954}

            height={560}

  

          />

        </div>

      </div>

  

      {/* Logo */}

      <div

    style={{

        position: "absolute", // Make the logo absolutely positioned

        top: "calc(57% - 45vh)", // Adjust this value based on the white box's position

        left: "calc(5% - 16px)", // Adjust this value based on white box width

        transform: "translateY(-50%)", // Align logo half above the border

        width: "144px",

        height: "144px",

        borderRadius: "50%", // Makes the logo circular

        backgroundColor: "#ffffff", // Optional

        display: "flex",

        alignItems: "center",

        justifyContent: "center",

        boxShadow: "0px 4px 4px rgba(0, 0, 0, 0.25)",

  }}

>

        <Image

          src="/images/logo-32x-32.png"

          alt="Logo"

          width={69.25}

          height={61.71}

          quality={100}

        />

      </div>

{/* Parent Right div */}

            <div

        style={{

            display: "flex", // Align child divs horizontally

            float:"right",

            flexDirection: "column",

            flexWrap: "nowrap", // Prevents wrapping to the next line

            alignItems: "flex-end", // Aligns content at the top

            height: "25vh", // Optional: Full-height layout

            maxWidth:"500px",

            position:"relative",

            width:"35vw",

            marginTop:"20vh",

            paddingRight:"10vw",

            marginRight:"10vw",

            overflow:"visible",

            backgroundColor:"black",

        }}

            >

            <h1

            style={{

                marginBottom: "1rem", // Space between title and paragraph

                fontSize: "2.5rem",

                fontWeight: "bold",

                textAlign: "left", // Align to the left

            }}

            >Design System →</h1>

            <p

            style={{

                fontSize: "1.2rem",

                lineHeight: "1.6", // Improve readability

                textAlign: "left", // Align to the left,

            }}

            >

                The design system contains all the information for reusable components and

            styles. It shows colors, typography styles, and components, including

            various component states if they&#039;re interactive.</p>

  

            <Image

        src="/images/emoji_1.png"

        width={39}

        height={39}

        style={{

        position: "absolute", // Position the emoji absolutely

        left: "0", // Align to the left edge

        top: "50%", // Center vertically

        transform: "translateY(-50%)", // Adjust for vertical centering

        }}

        />

  

            </div>

  
  

      </div>
```